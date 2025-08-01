---
title : "Chuẩn bị"
date: 2024-07-09
weight : 2
chapter : false
pre : " <b> 2. </b> "
---

**Nội dung:**
- [Cài đặt các công cụ cần thiết](1-Install-necessary-tools)
- [Source code](2-Set-up-source-code)
- [Cấu hình AWS IAM](3-Configuration-AWS-IAM)

## Tổng quan các bước triển khai ban đầu

Quá trình triển khai hệ thống quản lý Feature Flag trên AWS bắt đầu với ba bước quan trọng:

### 1. Cài đặt công cụ cần thiết
Ở bước này, bạn sẽ tiến hành cài đặt các công cụ hỗ trợ phát triển và quản lý hạ tầng như AWS CLI, Node.js, Git, VS Code và các extension liên quan. Việc chuẩn bị đầy đủ công cụ giúp đảm bảo quá trình làm việc với AWS và source code diễn ra thuận lợi, nhất quán trên nhiều môi trường.

### 2. Thiết lập mã nguồn
Sau khi đã có đầy đủ công cụ, bạn sẽ tiến hành lấy mã nguồn dự án từ repository, cấu hình các biến môi trường, cài đặt các package cần thiết và kiểm tra lại cấu trúc thư mục. Bước này giúp đảm bảo môi trường phát triển đồng bộ, sẵn sàng cho các thao tác tiếp theo như build, deploy hoặc tích hợp với các dịch vụ AWS.

### 3. Cấu hình AWS IAM
Để đảm bảo an toàn và phân quyền hợp lý khi truy cập các dịch vụ AWS, bạn sẽ tạo và cấu hình các user, group, role và policy trong AWS IAM. Việc này giúp kiểm soát quyền truy cập, bảo vệ tài nguyên và tuân thủ các nguyên tắc bảo mật trong quá trình phát triển cũng như vận hành hệ thống.

---

Những bước chuẩn bị này là nền tảng quan trọng, giúp quá trình triển khai các dịch vụ AWS phía sau được diễn ra suôn sẻ, an toàn và hiệu quả.