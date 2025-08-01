 ---
title : "AWS Cloudwatch"
date: 2024-07-16
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

## Tổng quan

ℹ️ **Information: Amazon CloudWatch** là dịch vụ theo dõi và quản lý cung cấp dữ liệu và thông tin định hướng hành động cho tài nguyên cơ sở hạ tầng và ứng dụng AWS, ứng dụng hybrid cũng như ứng dụng on-premises. Bạn có thể thu thập và truy cập tất cả dữ liệu về hiệu năng và hoạt động dưới hình thức logs và metrics trong cùng một nền tảng, thay vì theo dõi riêng lẻ (máy chủ, mạng hoặc cơ sở dữ liệu). **CloudWatch** cho phép bạn theo dõi end-to-end (ứng dụng, cơ sở hạ tầng và dịch vụ) và tận dụng cảnh báo, logs và dữ liệu sự kiện để tự động hóa các hành động và giảm Mean Time To Resolution (MTTR). Dịch vụ này giúp bạn giải phóng tài nguyên quan trọng và tập trung vào việc xây dựng các ứng dụng và giá trị kinh doanh.

---

## Tính năng chính

**CloudWatch** cung cấp thông tin định hướng hành động, hỗ trợ việc tối ưu hóa hiệu năng ứng dụng, quản lý sử dụng tài nguyên và hiểu rõ tình trạng hoạt động của toàn hệ thống. **CloudWatch** hiển thị dữ liệu metrics và logs chi tiết đến từng giây, lưu trữ dữ liệu trong 15 tháng (đối với metrics) và cho phép thực hiện các phép tính trên metrics.

💡 **Pro Tip:** Dịch vụ này cũng giúp bạn phân tích dữ liệu trên dữ liệu lịch sử nhằm tối ưu hóa chi phí và thu thập thông tin real-time để tối ưu hóa ứng dụng và tài nguyên cơ sở hạ tầng.

---

## Lợi ích chính

💡 **Pro Tip:** Với **Amazon CloudWatch**, bạn có thể:

- Giám sát toàn diện các tài nguyên AWS và ứng dụng của bạn
- Thiết lập cảnh báo thông minh dựa trên ngưỡng tùy chỉnh
- Tự động hóa phản hồi đối với các sự cố hoạt động
- Tạo bảng điều khiển trực quan để theo dõi hiệu suất
- Phân tích logs để khắc phục sự cố nhanh chóng

---

⚠️ **Warning:** Việc không thiết lập giám sát đầy đủ có thể dẫn đến thời gian ngừng hoạt động không lường trước, hiệu suất kém và chi phí cao hơn do sử dụng tài nguyên không hiệu quả.

### Nội dung

1. [Tạo CloudWatch Alarm](1-Create-CloudWatch-Alarm/)
2. [Tạo CloudWatch Dashboard](2-Create-CloudWatch-Dashboard/) 