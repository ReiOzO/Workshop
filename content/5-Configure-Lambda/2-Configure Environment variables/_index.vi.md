---
title: "Cấu hình Environment variables"
date: 2024-07-09
weight: 2
chapter: false
pre: " <b> 5.2 </b> "
---

- Chọn **Configuration**
- Click tab **Environment variables**
- Click **Edit**
- Add các biến:
- **Key**: APP_ID | **Value**: [ID của AppConfig application của bạn]
- **Key**: ENV_ID | **Value**: [ID của environment production]
- **Key**: PROFILE_ID | **Value**: [ID của configuration profile]
- Click **Save**

![MFA](/Workshop/images/5/13.jpg)

1.	Lấy APP_ID:
    - Vào AWS Console > AppConfig
    - Click vào application **MyFeatureFlagApp** của chúng ta
    - Trên URL của trình duyệt, bạn sẽ thấy một đoạn như:.../applications/abc123def...
    - Đoạn abc123def... chính là APP_ID
2.	Lấy ENV_ID:
    - Trong application vừa vào
    - Click tab **Environments**
    - Click vào environment **production**
    - Trên URL sẽ có dạng:.../environments/xyz789...
    - Đoạn xyz789... chính là ENV_ID
3.	Lấy PROFILE_ID:
    - Trong cùng application
    - Click tab **Configuration profiles**
    - Click vào profile **FeatureFlagDemo**
    - URL sẽ có dạng:.../configurationprofiles/def456...
    - Đoạn def456... chính là PROFILE_ID

![MFA](/Workshop/images/5/15.jpg)

