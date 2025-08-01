---
title: "Tạo Trigger cho Lambda Rollback"
date: 2024-07-09
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

### Tại sao phải tạo Trigger cho Lambda Rollback?

Việc tạo Trigger cho Lambda Rollback giúp tự động phát hiện và xử lý sự cố khi triển khai ứng dụng thất bại. Trigger sẽ kích hoạt hàm Lambda để thực hiện rollback (khôi phục lại trạng thái an toàn trước đó), đảm bảo hệ thống luôn ổn định và giảm thiểu thời gian gián đoạn dịch vụ.

### Bước 1: Vào Lambda Function

- Chọn function **feature-flag-rollback** đã tạo trước đó
- Trong tab Diagram, click vào nút **"+ Add trigger"**

![MFA](/Workshop/images/5/05.jpg)

### Bước 2: Chọn Trigger Type

- Trigger configuration: chọn **EventBridge (CloudWatch Events)**
- Existing rules: **feature-flag-rollback-trigger**

![MFA](/Workshop/images/5/06.jpg)
![MFA](/Workshop/images/5/07.jpg)

### Bước 3: Review và Create

- Review lại cấu hình
- Click **Add** để tạo trigger
![MFA](/Workshop/images/5/08.jpg)

### Test Trigger
1.	Vào CloudWatch → Alarms
2.	Chọn alarm AppConfig-GetHostedConfig-HighCallCount
    - Chọn **Action** → **Edit**
    - Giảm threshold xuống mức mà metric hiện tại chắc chắn vượt qua (ví dụ: nếu CallCount hiện tại là 10, đặt threshold là 3).
    - Nhấn Update alarm.
    - Đợi 1-2 phút, alarm sẽ chuyển sang trạng thái **In alarm** (màu đỏ).

![MFA](/Workshop/images/5/09.jpg)

![MFA](/Workshop/images/5/10.jpg)

3.	Vào **Lambda** → **Function** → **feature-flag-rollback** → **Test** Click "Test"

![MFA](/Workshop/images/5/11.jpg)

4.	Kiểm tra Lambda function logs để xem có được trigger không
    - Chọn tab Monitor hoặc CloudWatch Logs để kiểm tra log mới xuất hiện với timestamp gần nhất.
    - Nếu có log mới, nghĩa là Lambda đã được trigger tự động bởi Alarm thông qua EventBridge.

![MFA](/Workshop/images/5/12.jpg)

5.  Khôi phục lại threshold (nếu đã chỉnh): Sau khi test xong, nhớ chỉnh lại threshold về giá trị chuẩn để tránh cảnh báo giả.
