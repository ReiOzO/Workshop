---
title : "Dọn dẹp tài nguyên"
date: 2024-07-09
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

ℹ️ Information: Sau khi hoàn thành workshop, việc dọn dẹp tài nguyên là bước quan trọng để tránh phát sinh chi phí không cần thiết.

### 1. Dọn dẹp tài nguyên AWS AppConfig
#### Xoá Environment
1.  Trên thanh tìm kiếm dịch vụ AWS:
    - Nhập **AWS AppConfig**.
    - Chọn AWS AppConfig.

![MFA](/Workshop/images/7/0001.jpg)

2.  Trong AWS AppConfig:
    - Chọn **Applications** > **MyFeatureFlagApp**.
    - Chọn **Environments**
    - Ấn chọn **Delete environment**, xác nhận **Delete**.

![MFA](/Workshop/images/7/0002.jpg)
![MFA](/Workshop/images/7/0004.jpg)
![MFA](/Workshop/images/7/0007.jpg)

#### Xoá Configuration Profiles and Feature Flags
Trong AWS AppConfig:
- Chọn **Applications** > **MyFeatureFlagApp** > **FeatureFlagDemo**.

![MFA](/Workshop/images/7/0009.jpg)

- Ấn chọn **Delete version**, xác nhận **Delete**.

![MFA](/Workshop/images/7/0008.jpg)

- Sau khi xoá version, chọn **Action** > **Delete configuration profile**.

![MFA](/Workshop/images/7/0006.jpg)

#### Xoá Applications
Trong AWS AppConfig:
- Chọn **Applications** > **MyFeatureFlagApp**.
- Ấn chọn **Delete**, xác nhận **Delete**.

![MFA](/Workshop/images/7/0010.jpg)
![MFA](/Workshop/images/7/0003.jpg)

#### Xoá Deployment strategies
Trong AWS AppConfig:
- Chọn **Deployment strategies** > **workshop-gradual-rollout**.
- Ấn chọn **Delete**, xác nhận **Delete**.

![MFA](/Workshop/images/7/0026.jpg)
![MFA](/Workshop/images/7/0027.jpg)

### 2. Dọn dẹp tài nguyên AWS Cloudwatch
#### Xoá Alarms
1.  Trên thanh tìm kiếm dịch vụ AWS:
    - Nhập **CloudWatch**.
    - Chọn CloudWatch.

2.  Trong AWS CloudWatch:
    - Chọn **CloudWatch** > **Alarms**.
    - Chọn **AppConfig-GetHostedConfig-HighCallCount** > **Actions** > **Delete**.
    - Xác nhận **Delete**.

![MFA](/Workshop/images/7/0011.jpg)
![MFA](/Workshop/images/7/0012.jpg)

#### Xoá Dashboards
Trong AWS CloudWatch:
- Chọn **CloudWatch** > **Dashboards**.
- Chọn **FeatureFlags-Monitoring** > **Delete**.
- Xác nhận **Delete**.

![MFA](/Workshop/images/7/0013.jpg)
![MFA](/Workshop/images/7/0014.jpg)

#### Xoá Topics

1.  Trên thanh tìm kiếm dịch vụ AWS:
    - Nhập **SNS**.
    - Chọn **Simple Notification Service**.

![MFA](/Workshop/images/7/0015.jpg)

2.  Trong Amazon SNS:
    - Vào **Topics**.
    - Chọn **Default_CloudWatch_Alarms_Topic** > **Delete**.
    - Nhập **delete me**, xác nhận **Delete**.

![MFA](/Workshop/images/7/0016.jpg)
![MFA](/Workshop/images/7/0017.jpg)

#### Xoá Log groups
Trong AWS CloudWatch:
- Chọn **CloudWatch** > **Log groups**.
- Chọn **/aws/lambda/feature-flag-rollback** > **Actions** > **Delete log group(s)**.
- Xác nhận **Delete**.

![MFA](/Workshop/images/7/0018.jpg)
![MFA](/Workshop/images/7/0019.jpg)

⚠️ CloudWatch Metrics và Logs sẽ vẫn tồn tại trong hệ thống AWS của bạn tối đa 15 tháng theo chính sách lưu trữ mặc định.

### 3. Dọn dẹp tài nguyên AWS Lambda
#### Xoá Triggers
1.  Trên thanh tìm kiếm dịch vụ AWS:
    - Nhập **Lambda**.
    - Chọn Lambda.

2.  Trong AWS Lambda:
    - Chọn **Functions** > **feature-flag-rollback** > **Configuration**.
    - Chọn **EventBridge (CloudWatch Events): feature-flag-rollback-trigger**
    - Ấn chọn **Delete**, xác nhận **Delete**.

![MFA](/Workshop/images/7/0020.jpg)
![MFA](/Workshop/images/7/0021.jpg)

#### Xoá Lambda function
Trong AWS Lambda:
- Chọn **Functions** > **feature-flag-rollback** > **Actions** > **Delete**.
- Nhập **confirm**, xác nhận **Delete**.

![MFA](/Workshop/images/7/0022.jpg)
![MFA](/Workshop/images/7/0023.jpg)

#### Xoá CloudWatch Events Rule
1.  Trên thanh tìm kiếm dịch vụ AWS:
    - Nhập **EventBridge**.
    - Chọn **Amazon EventBridge**.

![MFA](/Workshop/images/4/01.jpg)

2.  Trong Amazon EventBridge:
    - Chọn **Rules**.
    - Chọn **feature-flag-rollback-trigger** > **Delete**.
    - Nhập **delete**, xác nhận **Delete**.

![MFA](/Workshop/images/7/0024.jpg)
![MFA](/Workshop/images/7/0025.jpg)

🔒 Security Note: Việc dọn dẹp tài nguyên không chỉ giúp tiết kiệm chi phí mà còn là biện pháp bảo mật tốt, giảm thiểu bề mặt tấn công tiềm ẩn trong môi trường AWS của bạn.
   
