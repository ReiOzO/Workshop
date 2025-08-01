---
title: "Giới thiệu"
date: 2024-07-16
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

## Sơ đồ tổng quan luồng hoạt động

![MFA](https://reiozo.github.io/Workshop/images/1/sodotongquan.png)

## Tổng quát về dự án Feature Flag Management

Dự án **Feature Flag Management** hướng tới việc xây dựng một hệ thống quản lý và kiểm soát việc phát hành các tính năng mới (feature flags) cho ứng dụng một cách an toàn, linh hoạt và tự động trên nền tảng AWS. Việc sử dụng feature flag giúp đội ngũ phát triển có thể bật/tắt, thử nghiệm, hoặc rollback các tính năng mà không cần triển khai lại toàn bộ ứng dụng, từ đó giảm thiểu rủi ro và tăng tốc độ đổi mới.

Hệ thống được thiết kế theo từng bước rõ ràng, tận dụng các dịch vụ chủ lực của AWS để đảm bảo tính tự động hóa, giám sát, an toàn và dễ dàng mở rộng. Dưới đây là các dịch vụ và bước thực hiện chính trong dự án:

---

### 1. Giới thiệu  
Cung cấp tổng quan về mục tiêu, lợi ích của việc quản lý feature flag và lý do lựa chọn AWS làm nền tảng triển khai.

### 2. Chuẩn bị  
Hướng dẫn chuẩn bị từng bước triển khai hệ thống quản lý feature flag trên AWS, từ khởi tạo tài nguyên đến cấu hình tự động hóa và giám sát.

### 3. AWS AppConfig  
Sử dụng **AWS AppConfig** để quản lý, triển khai và kiểm soát các feature flag một cách tập trung và an toàn. Bao gồm các bước:
- **Tạo Application:** Khởi tạo ứng dụng quản lý cấu hình.
- **Tạo Environment:** Xây dựng môi trường triển khai (dev, test, prod...).
- **Tạo Configuration:** Định nghĩa và lưu trữ các feature flag.
- **Tạo Deployment Strategy:** Thiết lập chiến lược rollout (triển khai dần, canary, linear...) để giảm thiểu rủi ro khi phát hành tính năng mới.

### 4. EventBridge Rule  
Thiết lập **AWS EventBridge Rule** để tự động phát hiện các sự kiện quan trọng (như lỗi, thay đổi trạng thái) và kích hoạt các quy trình xử lý tiếp theo, đảm bảo hệ thống luôn phản ứng kịp thời với các tình huống phát sinh.

### 5. Lambda  
Sử dụng **AWS Lambda** để tự động hóa các tác vụ như rollback khi phát hiện sự cố:
- **Tạo Lambda Function cho Automated Rollback:** Tự động khôi phục trạng thái an toàn khi có lỗi.
- **Tạo Trigger cho Lambda Rollback:** Kết nối Lambda với các sự kiện/alarms để tự động kích hoạt rollback.

### 6. AWS CloudWatch  
Tận dụng **Amazon CloudWatch** để giám sát, cảnh báo và trực quan hóa hoạt động của hệ thống:
- **Tạo CloudWatch Alarm:** Thiết lập cảnh báo khi có dấu hiệu bất thường.
- **Tạo CloudWatch Dashboard:** Xây dựng bảng điều khiển trực quan để theo dõi các chỉ số quan trọng.

### 7. Dọn dẹp tài nguyên  
Hướng dẫn cách xóa hoặc dọn dẹp các tài nguyên AWS sau khi hoàn thành thử nghiệm hoặc triển khai, giúp tối ưu chi phí và đảm bảo môi trường sạch sẽ.

---

## Mục tiêu

Dự án này giúp bạn từng bước xây dựng một hệ thống quản lý feature flag hiện đại, tự động hóa và an toàn trên AWS. Việc kết hợp các dịch vụ như AppConfig, EventBridge, Lambda và CloudWatch không chỉ giúp kiểm soát việc phát hành tính năng mà còn đảm bảo hệ thống luôn được giám sát, phản ứng nhanh với sự cố và dễ dàng mở rộng trong tương lai.
