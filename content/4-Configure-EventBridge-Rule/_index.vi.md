---
title : "EventBridge Rule"
date: 2024-07-09
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

## Tại sao cần tạo AWS EventBridge (CloudWatch Events)?

**AWS EventBridge** (trước đây gọi là CloudWatch Events) là một dịch vụ giúp bạn xây dựng các ứng dụng theo hướng sự kiện (event-driven) bằng cách kết nối các nguồn sự kiện với các mục tiêu xử lý (targets) như Lambda, Step Functions, SNS, SQS, v.v. Việc tạo EventBridge mang lại nhiều lợi ích quan trọng:

- **Tự động hóa quy trình vận hành:**  
  EventBridge cho phép bạn tự động hóa các hành động dựa trên sự kiện xảy ra trong hệ thống AWS hoặc từ các ứng dụng SaaS bên ngoài. Ví dụ: tự động kích hoạt Lambda khi có cảnh báo CloudWatch, hoặc gửi thông báo khi có thay đổi trạng thái tài nguyên.

- **Phản ứng nhanh với sự kiện:**  
  Bạn có thể thiết lập các quy tắc (rules) để phát hiện và phản hồi ngay lập tức với các sự kiện quan trọng như lỗi hệ thống, thay đổi cấu hình, hoặc các hành động của người dùng.

- **Tích hợp linh hoạt giữa các dịch vụ:**  
  EventBridge giúp kết nối và tích hợp nhiều dịch vụ AWS lại với nhau mà không cần phải viết nhiều mã xử lý phức tạp. Điều này giúp hệ thống của bạn mở rộng dễ dàng và linh hoạt hơn.

- **Giảm thiểu rủi ro và tăng tính ổn định:**  
  Bằng cách tự động hóa các phản ứng với sự kiện, bạn có thể giảm thiểu thời gian phát hiện và xử lý sự cố, từ đó tăng tính ổn định và độ tin cậy cho hệ thống.

- **Theo dõi và kiểm soát tốt hơn:**  
  EventBridge giúp bạn dễ dàng theo dõi các sự kiện quan trọng, ghi lại lịch sử sự kiện và kiểm soát các luồng công việc trong hệ thống.

**Tóm lại:**  
Việc tạo AWS EventBridge là cần thiết để xây dựng các hệ thống tự động, phản ứng nhanh với sự kiện, tối ưu hóa vận hành và nâng cao khả năng tích hợp giữa các dịch vụ AWS cũng như các ứng dụng bên ngoài. Dưới đây là các bước cơ bản để tạo 1 EventBridge Rule:

### Bước 1: Truy cập AWS EventBridge (CloudWatch Events)
- Đăng nhập AWS Console
- Vào dịch vụ **AWS EventBridge**

![MFA](/images/4/01.jpg?featherlight=false&width=90pc)

### Bước 2: Tạo Rule mới
- Chọn **Rules** ở menu bên trái
- Nhấn **Create rule**

![MFA](/images/4/02.jpg?featherlight=false&width=90pc)

### Bước 3: Thiết lập Rule
- **Name:** feature-flag-rollback-trigger
- **Description:** Trigger rollback when AppConfig metrics exceed thresholds
- **Event bus:** default
- **Rule type:** Rule with an event pattern

![MFA](/images/4/03.jpg?featherlight=false&width=90pc)

### Bước 4: Chọn Event pattern
- **Event pattern** chọn **Custom pattern (JSON editor)**
- Dán JSON sau vào:

```js
{
  "source": ["aws.cloudwatch"],
  "detail-type": ["CloudWatch Alarm State Change"],
  "detail": {
    "state": {
      "value": ["ALARM"]
    },
    "alarmName": [{
      "prefix": "AppConfig-"
    }, {
      "prefix": "FeatureFlag-"
    }]
  }
}
```

![MFA](/images/4/04.jpg?featherlight=false&width=90pc)

### Bước 5: Thêm Target
- **Target type:** AWS service
- **Select a target:** Lambda function
- **Function:** feature-flag-rollback
![MFA](/images/4/05.jpg?featherlight=false&width=90pc)

### Bước 6: Review & Create
- Kiểm tra lại thông tin.
- Nhấn **Create rule**
![MFA](/images/4/06.jpg?featherlight=false&width=90pc)


> **Lưu ý:** Rule này sẽ tự động trigger Lambda mỗi khi alarm có tên bắt đầu bằng AppConfig- hoặc FeatureFlag- chuyển sang trạng thái ALARM.