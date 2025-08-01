 ---
title : "Lambda"
date: 2024-07-16
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

## Tổng quan

ℹ️ **Information:** AWS Lambda là dịch vụ điện toán serverless cho phép bạn chạy mã mà không cần quản lý máy chủ. Trong quá trình triển khai ứng dụng hoặc cấu hình trên AWS, việc xảy ra lỗi hoặc sự cố là điều không thể tránh khỏi. Để đảm bảo hệ thống luôn ổn định và giảm thiểu thời gian gián đoạn, bạn nên thiết lập cơ chế **Automated Rollback** – tự động khôi phục về trạng thái an toàn trước đó khi phát hiện lỗi.

---

## Mục đích sử dụng Lambda cho Automated Rollback

- **Tự động hóa quá trình khôi phục:**  
  Lambda giúp tự động thực hiện các bước rollback khi phát hiện sự cố, loại bỏ thao tác thủ công, giảm thiểu rủi ro do con người gây ra.

- **Phản ứng nhanh với lỗi:**  
  Khi có cảnh báo hoặc sự kiện bất thường (ví dụ: CloudWatch Alarm phát hiện lỗi), Lambda sẽ được kích hoạt (Trigger) để xử lý rollback ngay lập tức, giúp hệ thống nhanh chóng trở lại trạng thái ổn định.

- **Tăng tính ổn định và tin cậy cho hệ thống:**  
  Việc tự động rollback giúp giảm thời gian ngừng dịch vụ, đảm bảo trải nghiệm người dùng và duy trì hoạt động kinh doanh liên tục.

---

## Tại sao cần tạo Trigger cho Lambda Rollback?

- **Kích hoạt tự động:**  
  Trigger (thường là CloudWatch Alarm, EventBridge Rule, v.v.) giúp Lambda được gọi tự động khi có sự kiện hoặc điều kiện nhất định xảy ra, đảm bảo quá trình rollback diễn ra kịp thời mà không cần can thiệp thủ công.

- **Giám sát và phản ứng chủ động:**  
  Trigger giúp hệ thống chủ động phát hiện và xử lý sự cố, giảm thiểu thiệt hại và rủi ro cho ứng dụng.

---

> **Lưu ý:** Việc kết hợp Lambda Function với Trigger là giải pháp hiệu quả để tự động hóa quy trình rollback, nâng cao độ tin cậy và an toàn cho hệ thống AWS của bạn.

### Nội dung

1. [Tạo Lambda Function](1-Create-Lambda-Function-for-Automated-Rollback/)
2. [Cấu hình Environment variables](2-Configure-Environment-variables/) 
3. [Tạo Trigger cho Lambda](3-Create-Trigger-for-Lambda-Rollback/) 