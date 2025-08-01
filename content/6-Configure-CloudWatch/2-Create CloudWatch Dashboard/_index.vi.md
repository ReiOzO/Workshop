---
title : "Tạo CloudWatch Dashboard"
date: 2024-07-16
weight : 2
chapter : false
pre : " <b> 6.2 </b> "
---

## Tạo CloudWatch Dashboard

ℹ️ **Information:** Amazon CloudWatch Dashboards là công cụ trực quan hóa mạnh mẽ cho phép bạn tạo các bảng điều khiển tùy chỉnh để giám sát tài nguyên AWS trong thời gian thực. Dashboards giúp tập hợp các metrics, logs và alarms quan trọng vào một nơi duy nhất, tạo điều kiện thuận lợi cho việc giám sát và phân tích hệ thống. Dưới đây là các bước tạo dashboard:

### Bước 1: Truy cập Amazon CloudWatch
- Đăng nhập AWS Console
- Vào dịch vụ **CloudWatch**

### Bước 2: Chọn mục Dashboards
- Chọn **Dashboards** ở menu bên trái
- Nhấn **Create dashboard**

![MFA](/Workshop/images/6/013.jpg)

### Bước 3: Đặt tên cho dashboard
- Nhập tên dashboard (ví dụ: **FeatureFlags-Monitoring**) và nhấn **Create dashboard**

![MFA](/Workshop/images/6/014.jpg)

### Bước 4: Thêm widget vào dashboard
- Chọn loại widget (Line, Stacked area, Number, Text...)
- Chọn **Configure** để chọn chỉ số hoặc log muốn hiển thị
- Tùy chỉnh giao diện, thời gian, màu sắc...

#### Widget 1 - API Latency Monitor:
1. Click **Add widget** > Chọn **Metrics** > **Line**
2. Tìm và chọn các metrics: **Usage** > **By AWS Resource**
    - AWS AppConfig - GetHostedConfigurationVersion
    - AWS AppConfig - GetConfigurationProfile
    - AWS AppConfig - ListHostedConfigurationVersions
3. Graphed metrics:
    - Title: **API Response Time**
    - Period: **5 minutes**
    - Statistic: **Average**
4. Click **Create widget**

![MFA](/Workshop/images/6/015.jpg)
![MFA](/Workshop/images/6/016.jpg)
![MFA](/Workshop/images/6/017.jpg)
![MFA](/Workshop/images/6/018.jpg)

#### Widget 2 - Deployment Monitoring:
1. Click **Add widget** > Chọn **Metrics** > **Line**
2. Tìm và chọn các metrics: **Usage** > **By AWS Resource**
    - AWS AppConfig - StartDeployment
    - AWS AppConfig - StopDeployment
    - AWS AppConfig - GetDeployment
3. Graphed metrics:
    - Title: **Deployment Monitoring**
    - Period: **1 minute**
    - Statistic: **Sum**
4. Click **Create widge**

![MFA](/Workshop/images/6/019.jpg)

#### Widget 3 - Resource Count:
1. Click **Add widget** > Chọn **Metrics** > **Number**
2. Tìm và chọn các metrics: **Usage** > **By AWS Resource**
    - AWS AppConfig - Application
    - AWS AppConfig - DeploymentStrategy
3. Graphed metrics:
    - Title: **Resource Count**
    - Period: **5 minutes**
    - Statistic: **Average**
4. Click **Create widge**

![MFA](/Workshop/images/6/020.jpg)
![MFA](/Workshop/images/6/021.jpg)

#### Widget 4 - Configuration Changes:
1. Click **Add widget** > Chọn **Metrics** > **Line**
2. Tìm và chọn các metrics: **Usage** > **By AWS Resource**
    - AWS AppConfig - CreateHostedConfigurationVersion
    - AWS AppConfig - UpdateApplication
3. Graphed metrics:
    - Title: **Configuration Changes**
    - Period: **1 minute**
    - Statistic: **Sum**
4. Click **Create widge**

![MFA](/Workshop/images/6/022.jpg)

#### Widget 5 - RollbackTriggered:
1. Click **Add widget** > Chọn **Metrics** > **Number**
2. Tìm và chọn các metrics: **Lambda** > **By Function Name**
    - feature-flag-rollback - Invocations
    - feature-flag-rollback - Errors
    - feature-flag-rollback - Duration
3. Graphed metrics:
    - Period: **5 minute**
    - Statistic: **Average**
4. Click **Create widge**

![MFA](/Workshop/images/6/024.jpg)

### Bước 5: Lưu dashboard
- Nhấn **Save dashboard** để hoàn tất

![MFA](/Workshop/images/6/025.jpg)

> **Lưu ý:** Bạn có thể thêm nhiều widget để giám sát nhiều dịch vụ và chỉ số khác nhau trên cùng một dashboard.

