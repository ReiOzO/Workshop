---
title : " Tạo Deployment Strategy"
date: 2024-07-09
weight : 4
chapter : false
pre : " <b> 3.4 </b> "
---

1. Chọn tab **Deployment strategies**
2. Click **Create deployment strategy**

![MFA](/Workshop/images/3/0020.jpg)

3. Điền thông tin:
    - Name: **workshop-gradual-rollout**
    - Description: **Gradual feature rollout strategy**
    - Deployment type: **Linear**
    - Step percentage: **25%**
    - Deployment time: **2 minutes**
    - Bake time: **3 minutes**

4. Click **Create deployment strategy**

![MFA](/Workshop/images/3/0019.jpg)

### Deploy Configuration

1. Quay lại Configuration profile
2. Click **Start deployment**

![MFA](/Workshop/images/3/0021.jpg)

3. Chọn:
    - Environment: **production**
    - Hosted configuration version: **1**
    - Deployment strategy: **workshop-gradual-rollout**

4. Click **Start deployment**

![MFA](/Workshop/images/3/0022.jpg)

#### Deployment sẽ diễn ra theo timeline (Lý thuyết)
- ⏰ 0 min: Deployment starts (0%)
- ⏰ 2 min: 25% users receive new feature flags
- ⏰ 4 min: 50% users receive new feature flags
- ⏰ 6 min: 75% users receive new feature flags 
- ⏰ 8 min: 100% users receive new feature flags 
- ⏰ 11 min: Bake time complete ✅

5. Deployment theo timeline thực tế

![MFA](/Workshop/images/3/0023.jpg)
![MFA](/Workshop/images/3/0024.jpg)
