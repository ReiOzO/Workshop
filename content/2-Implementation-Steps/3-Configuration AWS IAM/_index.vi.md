---
title : "Cấu hình AWS IAM"
date: 2024-07-09
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

## Cấu hình AWS IAM

Trong phần này, chúng ta sẽ cấu hình AWS Identity and Access Management (IAM) để đảm bảo bảo mật cho hệ thống. IAM là dịch vụ quan trọng giúp quản lý quyền truy cập vào các tài nguyên AWS một cách an toàn.

### Tổng quan về AWS IAM

AWS IAM cho phép bạn:
- Quản lý người dùng, nhóm và vai trò
- Cấp phát quyền truy cập đến các tài nguyên AWS
- Thiết lập xác thực đa yếu tố (MFA)
- Thiết lập chính sách mật khẩu
- Phân tích quyền truy cập để đảm bảo tuân thủ nguyên tắc đặc quyền tối thiểu

### Tạo AWS Access Key ID và Secret Access Key
1. Đăng nhập vào AWS Management Console
2. Truy cập vào dịch vụ **IAM** (Identity and Access Management)

![MFA](/Workshop/images/2/001.jpg?featherlight=false&width=90pc)

3. Chọn "**Users**" ở menu bên trái
4. Chọn user của bạn (hoặc tạo user mới nếu chưa có)
5. Chọn tab "**Security credentials**"
6. Nhấp vào "**Create access key**"

![MFA](/images/2/002.jpg?featherlight=false&width=90pc)
![MFA](/images/2/003.jpg?featherlight=false&width=90pc)

7. Lưu lại "**Access key**" và "**Secret access key**"
8. Tải xuống file .csv chứa access key (nếu cần)
9. Nhấn "**Done**" để hoàn thành
![MFA](/images/2/004.jpg?featherlight=false&width=90pc)

**Lưu ý quan trọng**: Secret Access Key sẽ chỉ được hiển thị một lần tại thời điểm tạo. Hãy đảm bảo lưu trữ nó ở nơi an toàn.

