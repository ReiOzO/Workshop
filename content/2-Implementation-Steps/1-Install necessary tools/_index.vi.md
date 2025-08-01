---
title : "Cài đặt các công cụ cần thiết"
date: 2024-07-09
weight : 1
chapter : false
pre : " <b> 2.1 </b> "
---

## Kiến trúc tổng quan của project

Project sử dụng kiến trúc phân tầng:
- **Tầng Cấu hình:** AWS AppConfig để quản lý và triển khai feature flag, cấu hình động cho ứng dụng.
- **Tầng Thực thi:** AWS Lambda functions thực hiện các tác vụ cụ thể
- **Tầng Monitoring:** CloudWatch cho logging và monitoring
- **Tầng Thông báo:** SNS/Email/Slack cho notifications

### Cài đặt công cụ phát triển

Để chuẩn bị môi trường phát triển trên máy local, chúng ta cần cài đặt một số công cụ sau:

1. **AWS CLI**: Giao diện dòng lệnh AWS để tương tác với các dịch vụ AWS
2. **Node.js và npm**: Để phát triển serverless functions bằng JavaScript
3. **Git**: Để quản lý mã nguồn
4. **IDE hoặc text editor**: Visual Studio Code, IntelliJ, hoặc bất kỳ IDE nào bạn quen thuộc

#### Cài đặt AWS CLI

AWS CLI là công cụ dòng lệnh giúp bạn tương tác với các dịch vụ AWS thông qua các lệnh trong terminal.

**Cài đặt trên Windows:**

```bash
# Sử dụng MSI installer
# Tải xuống từ https://aws.amazon.com/cli/
```

**Kiểm tra cài đặt:**

```bash
aws --version
```

#### Cài đặt Node.js và npm

**Cài đặt trên Windows/macOS/Linux:**

Tải và cài đặt từ [nodejs.org](https://nodejs.org/)

Kiểm tra cài đặt:

```bash
node --version
npm --version
```

#### Cài đặt Git

**Cài đặt trên Windows:**

Tải và cài đặt từ [git-scm.com](https://git-scm.com/download/win)

**Kiểm tra cài đặt:**

```bash
git --version
```

### Kết luận

Sau khi hoàn thành các bước trên, bạn đã có một môi trường phát triển local với các công cụ cần thiết để làm việc với AWS. Trong phần tiếp theo, chúng ta sẽ cấu hình AWS CLI để kết nối với tài khoản AWS của bạn. 