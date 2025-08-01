---
title: "Tạo Lambda Function cho Automated Rollback"
date: 2024-07-09
weight: 1
chapter: false
pre: " <b> 5.1 </b> "
---

### Tại sao phải tạo Trigger và Lambda Function cho Automated Rollback?

Việc tạo Trigger và Lambda Function cho Automated Rollback giúp hệ thống tự động phát hiện lỗi và khôi phục về trạng thái an toàn trước đó mà không cần can thiệp thủ công. Điều này đảm bảo ứng dụng luôn ổn định, giảm thiểu rủi ro và thời gian gián đoạn dịch vụ.

### Bước 1: Truy cập AWS Lambda

- Đăng nhập AWS Console
- Vào dịch vụ **Lambda**

![MFA](/images/5/01.jpg?featherlight=false&width=90pc)

### Bước 2: Chọn mục Functions

- Chọn **Functions** ở menu bên trái
- Nhấn **Create function**

![MFA](/images/5/02.jpg?featherlight=false&width=90pc)

1. Điền thông tin:
   - Chọn **Author from scratch**
   - Function name: **feature-flag-rollback**
   - Runtime: **Node.js 22.x**
   - Architecture: x86_64
2. Click "Create function"

![MFA](/images/5/03.jpg?featherlight=false&width=90pc)

### Bước 3: Deloy code

- Copy code từ **aws-config/lambda/rollback-function.js**.
- Click **Deploy** để lưu code.

```js
{
  const {
    AppConfigClient,
    StartConfigurationSessionCommand,
    GetConfigurationCommand,
    CreateHostedConfigurationVersionCommand,
    StartDeploymentCommand,
  } = require("@aws-sdk/client-appconfig");
  const {
    CloudWatchClient,
    PutMetricDataCommand,
  } = require("@aws-sdk/client-cloudwatch");
  const { SNSClient, PublishCommand } = require("@aws-sdk/client-sns");

  // Khởi tạo client
  const appConfig = new AppConfigClient({ region: process.env.AWS_REGION });
  const cloudWatch = new CloudWatchClient({ region: process.env.AWS_REGION });
  const sns = new SNSClient({ region: process.env.AWS_REGION });

  /**
   * Lambda function for automated feature flag rollback
   */
  exports.handler = async (event) => {
    console.log("Received event:", JSON.stringify(event, null, 2));

    try {
      // Parse CloudWatch alarm event
      const message = JSON.parse(event.Records[0].Sns.Message);
      const alarmName = message.AlarmName;
      const alarmState = message.NewStateValue;
      const alarmReason = message.NewStateReason;

      // Extract feature flag name from alarm name
      const featureFlagName = extractFeatureFlagName(alarmName);

      if (!featureFlagName) {
        console.error(
          "Could not extract feature flag name from alarm:",
          alarmName
        );
        return {
          statusCode: 400,
          body: JSON.stringify({
            error: "Invalid alarm name format",
          }),
        };
      }

      console.log(`Processing alarm for feature flag: ${featureFlagName}`);
      console.log(`Alarm state: ${alarmState}`);

      // Only process ALARM state (not OK or INSUFFICIENT_DATA)
      if (alarmState !== "ALARM") {
        console.log("Alarm state is not ALARM, skipping rollback");
        return {
          statusCode: 200,
          body: JSON.stringify({
            message: "Alarm state is not ALARM, no action taken",
          }),
        };
      }

      // Get current feature flag configuration
      const currentConfig = await getFeatureFlagConfiguration();

      if (
        !currentConfig ||
        !currentConfig.flags ||
        !currentConfig.flags[featureFlagName]
      ) {
        console.error(
          `Feature flag ${featureFlagName} not found in configuration`
        );
        return {
          statusCode: 404,
          body: JSON.stringify({
            error: "Feature flag not found",
          }),
        };
      }

      // Perform rollback
      await rollbackFeatureFlag(featureFlagName, currentConfig);

      // Send notification
      await sendRollbackNotification(featureFlagName, alarmReason);

      // Log rollback metrics
      await logRollbackMetrics(featureFlagName);

      return {
        statusCode: 200,
        body: JSON.stringify({
          message: `Successfully rolled back feature flag: ${featureFlagName}`,
          timestamp: new Date().toISOString(),
        }),
      };
    } catch (error) {
      console.error("Error in rollback function:", error);

      // Send error notification
      await sendErrorNotification(error.message);

      return {
        statusCode: 500,
        body: JSON.stringify({
          error: "Rollback failed",
          message: error.message,
        }),
      };
    }
  };

  /**
   * Extract feature flag name from alarm name
   */
  function extractFeatureFlagName(alarmName) {
    // Expected format: FeatureFlag-{flagName}-ErrorRate
    const match = alarmName.match(/^FeatureFlag-(.+)-ErrorRate$/);
    return match ? match[1] : null;
  }

  /**
   * Get current feature flag configuration from AppConfig
   */
  async function getFeatureFlagConfiguration() {
    try {
      const params = {
        ApplicationIdentifier: process.env.APPCONFIG_APPLICATION,
        EnvironmentIdentifier: process.env.APPCONFIG_ENVIRONMENT,
        ConfigurationProfileIdentifier: process.env.APPCONFIG_PROFILE,
        ClientId: `rollback-lambda-${Date.now()}`,
      };

      const session = await appConfig
        .startConfigurationSession(params)
        .promise();

      const configParams = {
        ConfigurationToken: session.InitialConfigurationToken,
      };

      const result = await appConfig.getConfiguration(configParams).promise();

      if (result.Configuration) {
        return JSON.parse(result.Configuration.toString());
      }

      return null;
    } catch (error) {
      console.error("Error getting feature flag configuration:", error);
      throw error;
    }
  }

  /**
   * Rollback feature flag by disabling it
   */
  async function rollbackFeatureFlag(flagName, currentConfig) {
    try {
      // Disable the feature flag
      currentConfig.flags[flagName].enabled = false;
      currentConfig.flags[flagName].rolloutPercentage = 0;
      currentConfig.flags[flagName].metadata.lastRollback =
        new Date().toISOString();
      currentConfig.flags[flagName].metadata.rollbackReason =
        "Automated rollback due to alarm";

      // Update version
      currentConfig.version = generateVersion();
      currentConfig.lastUpdated = new Date().toISOString();

      // Create new configuration version
      const createParams = {
        ApplicationId: process.env.APPCONFIG_APPLICATION,
        ConfigurationProfileId: process.env.APPCONFIG_PROFILE,
        Content: JSON.stringify(currentConfig),
        ContentType: "application/json",
        Description: `Automated rollback of ${flagName} due to alarm`,
      };

      const versionResult = await appConfig
        .createHostedConfigurationVersion(createParams)
        .promise();

      // Start immediate deployment
      const deployParams = {
        ApplicationId: process.env.APPCONFIG_APPLICATION,
        EnvironmentId: process.env.APPCONFIG_ENVIRONMENT,
        ConfigurationProfileId: process.env.APPCONFIG_PROFILE,
        ConfigurationVersion: versionResult.VersionNumber.toString(),
        DeploymentStrategyId: "AppConfig.AllAtOnce",
        Description: `Emergency rollback of ${flagName}`,
      };

      await appConfig.startDeployment(deployParams).promise();

      console.log(`Successfully rolled back feature flag: ${flagName}`);
    } catch (error) {
      console.error("Error rolling back feature flag:", error);
      throw error;
    }
  }

  /**
   * Send rollback notification
   */
  async function sendRollbackNotification(flagName, reason) {
    try {
      const message = {
        subject: `🚨 Feature Flag Rollback: ${flagName}`,
        message: `Feature flag "${flagName}" has been automatically rolled back due to alarm.\n\nReason: ${reason}\n\nTime: ${new Date().toISOString()}\n\nPlease investigate and take appropriate action.`,
        flagName: flagName,
        timestamp: new Date().toISOString(),
        action: "rollback",
      };

      const params = {
        TopicArn: process.env.SNS_TOPIC_ARN,
        Message: JSON.stringify(message),
        Subject: message.subject,
      };

      await sns.publish(params).promise();
      console.log("Rollback notification sent");
    } catch (error) {
      console.error("Error sending rollback notification:", error);
    }
  }

  /**
   * Send error notification
   */
  async function sendErrorNotification(errorMessage) {
    try {
      const message = {
        subject: "❌ Feature Flag Rollback Failed",
        message: `Automated rollback failed with error: ${errorMessage}\n\nTime: ${new Date().toISOString()}\n\nPlease investigate immediately.`,
        timestamp: new Date().toISOString(),
        action: "rollback_failed",
      };

      const params = {
        TopicArn: process.env.SNS_TOPIC_ARN,
        Message: JSON.stringify(message),
        Subject: message.subject,
      };

      await sns.publish(params).promise();
    } catch (error) {
      console.error("Error sending error notification:", error);
    }
  }

  /**
   * Log rollback metrics to CloudWatch
   */
  async function logRollbackMetrics(flagName) {
    try {
      const params = {
        Namespace: "FeatureFlags",
        MetricData: [
          {
            MetricName: "AutomatedRollback",
            Value: 1,
            Unit: "Count",
            Timestamp: new Date(),
            Dimensions: [
              {
                Name: "FeatureFlagName",
                Value: flagName,
              },
            ],
          },
        ],
      };

      await cloudWatch.putMetricData(params).promise();
      console.log("Rollback metrics logged");
    } catch (error) {
      console.error("Error logging rollback metrics:", error);
    }
  }

  /**
   * Generate version string
   */
  function generateVersion() {
    const now = new Date();
    return `${now.getFullYear()}.${
      now.getMonth() + 1
    }.${now.getDate()}.${now.getHours()}${now.getMinutes()}`;
  }
}
```

![MFA](/images/5/04.jpg?featherlight=false&width=90pc)
![MFA](/images/5/05.jpg?featherlight=false&width=90pc)