---
title : "Source code"
date: 2024-07-09
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

## Cấu hình AWS CLI

Trong phần này, chúng ta sẽ cấu hình AWS CLI (Command Line Interface) để có thể tương tác với các dịch vụ AWS từ môi trường local. AWS CLI là công cụ dòng lệnh quan trọng giúp chúng ta quản lý các tài nguyên AWS một cách tự động và hiệu quả.

### Tại sao cần cấu hình AWS CLI?

AWS CLI cho phép chúng ta thực hiện nhiều thao tác với AWS mà không cần sử dụng giao diện đồ họa (AWS Management Console). Điều này đặc biệt hữu ích khi:
- Tự động hóa quy trình triển khai
- Tích hợp với các pipeline CI/CD
- Quản lý tài nguyên theo hướng Infrastructure as Code (IaC)
- Thực hiện các tác vụ quản trị lặp đi lặp lại

### Chuẩn bị các thông tin cần thiết

Trước khi cấu hình AWS CLI, chúng ta cần chuẩn bị các thông tin sau:
1. **AWS Access Key ID**: Mã định danh cho người dùng AWS IAM
2. **AWS Secret Access Key**: Khóa bí mật tương ứng với Access Key ID
3. **AWS Region**: Khu vực AWS mà bạn muốn làm việc chủ yếu
4. **Output Format**: Định dạng đầu ra cho kết quả từ AWS CLI (json, yaml, text, table)

Để có được AWS Access Key ID và Secret Access Key, bạn cần:
1. Đăng nhập vào AWS Management Console
2. Truy cập vào dịch vụ **IAM** (Identity and Access Management)
3. Chọn "**Users**" ở menu bên trái
4. Chọn user của bạn (hoặc tạo user mới nếu chưa có)
5. Chọn tab "**Security credentials**"
6. Nhấp vào "**Create access key**"

**Lưu ý quan trọng**: Secret Access Key sẽ chỉ được hiển thị một lần tại thời điểm tạo. Hãy đảm bảo lưu trữ nó ở nơi an toàn.

### Cài đặt AWS CLI

Nếu bạn chưa cài đặt AWS CLI, hãy làm theo hướng dẫn dưới đây:

**Trên Windows:**
1. Tải xuống bộ cài đặt MSI từ [trang chủ AWS CLI](https://aws.amazon.com/cli/)
2. Chạy bộ cài đặt và làm theo các bước

Kiểm tra cài đặt:

```bash
aws --version
```

Kết quả sẽ hiển thị phiên bản AWS CLI, ví dụ: `aws-cli/2.27.50 Python/3.13.4 Windows/11 exe/AMD64`

### Cấu hình AWS CLI cơ bản

Để cấu hình AWS CLI, chúng ta sẽ sử dụng lệnh `aws configure`:

```bash
aws configure
```

Hệ thống sẽ yêu cầu nhập các thông tin sau:
- AWS Access Key ID: Nhập Access Key ID của bạn
- AWS Secret Access Key: Nhập Secret Access Key của bạn
- Default region name: Nhập khu vực AWS (ví dụ: us-east-1, ap-southeast-1)
- Default output format: Nhập định dạng đầu ra mong muốn (json, yaml, text, table)

Ví dụ:

```
AWS Access Key ID [None]: "your_access_key_id"
AWS Secret Access Key [None]: "your_secret_access_key"
Default region name [None]: us-east-1
Default output format [None]: json
```

## Clone project về máy
### Clone repository
```bash
git clone https://github.com/ReiOzO/Project-FeatureFlagManagement.git
cd Project-FeatureFlagManagement
```

### Backend setup
```bash
cd backend
npm install
npm run setup-aws
npm run dev
```

### Frontend setup
```bash
cd frontend
npm install
npm start
```

### AWS configuration
```bash
cd aws-config
./deploy-appconfig.sh
./setup-cloudwatch.sh
```