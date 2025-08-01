---
title : "Tạo CloudWatch Alarm"
date: 2024-07-09
weight : 1
chapter : false
pre : " <b> 6.1 </b> "
---

#### Hướng dẫn Thiết lập CloudWatch Alarm

ℹ️ **Information:** CloudWatch Alarm giúp bạn giám sát các chỉ số (metrics) và tự động gửi cảnh báo khi vượt ngưỡng. Dưới đây là các bước tạo một CloudWatch Alarm cơ bản:

### Bước 1: Truy cập Amazon CloudWatch
- Đăng nhập AWS Console
- Vào dịch vụ **CloudWatch**

![MFA](/Workshop/images/6/001.jpg)

### Bước 2: Chọn mục Alarms
- Chọn **Alarms** > **All alarms** ở menu bên trái
- Nhấn **Create alarm**

![MFA](/Workshop/images/6/002.jpg)

### Bước 3: Chọn chỉ số cần giám sát
- Chọn **Select metric**
- Chọn metric phù hợp **Usage > By AWS Resource** (ví dụ: error rate, latency, hoặc bất kỳ metric nào bạn muốn giám sát để rollback).
- Nhấn **Select metric**

![MFA](/Workshop/images/6/003.jpg)
![MFA](/Workshop/images/6/004.jpg)
![MFA](/Workshop/images/6/005.jpg)

### Bước 4: Đặt điều kiện cảnh báo
<!-- - Đặt điều kiện alarm (ví dụ: nếu error rate > 10 trong 5 phút). -->
1. Metric:
    - Metric name: **CallCount**
    - Type: **API**
    - Resource: **GetHostedConfigurationVersion**
    - Service: **AWS AppConfig**
    - Statistic: **Sum**
    - Period: **5 minutes**
2. Conditions:
    - Threshold type: **Static**
    - Whenever CallCount is: **Greater**
    - than: 10
3. Additional configuration:
    - Datapoints to alarm: **1** out of **1**
    - Missing data treatment: Treat missing data as missing
4. Click "Next" để tiếp tục

![MFA](/Workshop/images/6/006.jpg)
![MFA](/Workshop/images/6/007.jpg)

### Bước 5: Thiết lập hành động khi cảnh báo
- Chọn gửi thông báo qua SNS topic hoặc email
    - Alarm state trigger: **In alarm**
    - SNS option: **Create new topic**
    - Topic name: **Default_CloudWatch_Alarms_Topic**
    - Email: **Your_email** (Nhập email muốn nhập cảnh báo)
- Có thể chọn tự động thực hiện hành động (stop, terminate instance...)
![MFA](/Workshop/images/6/008.jpg)

- Ở phần Actions, chọn Add Lambda action
    - Alarm state trigger: **In alarm**
    - Function Type: **Select Lambda Function from the signed in account**
    - Choose a function: **feature-flag-rollback** (đã tạo trước đó)

![MFA](/Workshop/images/6/009.jpg)

### Bước 6: Đặt tên và tạo alarm
- Đặt tên cho alarm: **AppConfig-GetHostedConfig-HighCallCount**
- Kiểm tra lại thông tin và nhấn **Create alarm**
![MFA](/Workshop/images/6/031.jpg)
![MFA](/Workshop/images/6/011.jpg)
![MFA](/Workshop/images/6/012.jpg)

> **Lưu ý:** Bạn có thể tạo nhiều alarm cho nhiều chỉ số khác nhau để giám sát toàn diện hệ thống.

**Kết quả**
![MFA](/Workshop/images/6/026.jpg)

### Bước 7:Xác nhận Email
- Đăng nhập vào Email bạn đã dùng để thiết lập cảnh báo trước đó. Bạn sẽ thấy một email được gửi tới từ AWS Notification.
- Ấn chọn **Confirm subscription**.

![MFA](/Workshop/images/6/030.jpg)
![MFA](/Workshop/images/6/029.jpg)

🔒 Security Note: Việc xác nhận đăng ký SNS không chỉ kích hoạt thông báo mà còn là một biện pháp bảo mật, đảm bảo rằng chỉ những người dùng được ủy quyền mới nhận được thông báo về trạng thái hệ thống.

