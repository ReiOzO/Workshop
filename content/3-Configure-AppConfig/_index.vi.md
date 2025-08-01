---
title : "AWS AppConfig"
date: 2024-07-16
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

## Tổng quan

ℹ️ **Information: AWS AppConfig** là một dịch vụ thuộc AWS Systems Manager giúp bạn triển khai, quản lý và kiểm soát các cấu hình động (dynamic configuration) cho ứng dụng một cách an toàn và linh hoạt. Một trong những ứng dụng phổ biến nhất của AppConfig là quản lý **Feature Flag** – cho phép bạn bật/tắt, kiểm soát tính năng mới mà không cần phải triển khai lại mã nguồn.

---

## Mục đích sử dụng AWS AppConfig để quản lý Feature Flag

- **Triển khai tính năng mới một cách an toàn:**  
  Feature Flag giúp bạn kiểm soát việc phát hành tính năng mới cho từng nhóm người dùng, giảm rủi ro khi triển khai và dễ dàng rollback nếu có sự cố.

- **Tăng tốc độ phát triển và thử nghiệm:**  
  Cho phép đội ngũ phát triển thử nghiệm A/B, canary release hoặc gradual rollout mà không cần thay đổi mã nguồn hay tái khởi động dịch vụ.

- **Quản lý cấu hình tập trung:**  
  Tất cả các cấu hình và feature flag được quản lý tập trung, dễ dàng kiểm soát, theo dõi và cập nhật.

- **Đảm bảo an toàn khi thay đổi:**  
  AppConfig hỗ trợ kiểm tra, xác thực cấu hình trước khi áp dụng, giúp giảm thiểu lỗi do cấu hình sai.

---

## Lợi ích chính

💡 **Pro Tip:** Với **AWS AppConfig**, bạn có thể:

- Bật/tắt tính năng theo thời gian thực mà không cần deploy lại ứng dụng
- Giảm thiểu rủi ro khi phát hành tính năng mới
- Dễ dàng rollback khi có sự cố
- Hỗ trợ kiểm thử, A/B testing, canary release hiệu quả
- Quản lý cấu hình động cho nhiều môi trường (dev, test, prod) một cách linh hoạt

---

⚠️ **Warning:** Nếu không sử dụng giải pháp quản lý feature flag chuyên nghiệp, việc bật/tắt tính năng hoặc thay đổi cấu hình có thể gây ra lỗi hệ thống, downtime hoặc trải nghiệm người dùng không nhất quán.

### Nội dung

1. [Tạo Application](1-Create-Application/)
2. [Tạo Environment](2-Create-Environment/)
3. [Tạo Configuration](3-Create-Hosted-Configuration-Profile/)
4. [Tạo Deployment Strategy](4-Create-Deployment-Strategy/)