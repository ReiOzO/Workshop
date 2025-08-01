---
title : "Tạo Configuration"
date: 2024-07-09
weight : 3
chapter : false
pre : " <b> 3.3 </b> "
---

## Tạo Hosted Configuration Profile (JSON chứa feature flags)

1. Trong application, chọn tab **Configuration profiles**
2. Click **Create configuration profile**

![MFA](/Workshop/images/3/0015.jpg)

### Step 1: Select configuration type
- Configuration options: **Freeform configuration**
- Configuration profile name: **FeatureFlagDemo**

![MFA](/Workshop/images/3/0016.jpg)

### Step 2: Specify configuration data
- Configuration definition: **AWS AppConfig hosted configuration**
- Content: **JSON**

![MFA](/Workshop/images/3/0017.jpg)

```js
{
  "version": "1.0.0",
  "lastUpdated": "2025-07-12T14:42:04.610Z",
  "flags": {
    "dark-mode": {
      "enabled": true,
      "rolloutPercentage": 100,
      "targeting": {
        "userGroups": [],
        "userIds": []
      },
      "variants": [
        {
          "name": "control",
          "weight": 50
        },
        {
          "name": "treatment",
          "weight": 50
        }
      ],
      "metadata": {
        "description": "Dark mode feature",
        "owner": "admin",
        "createdAt": "2025-07-12T00:00:00Z"
      }
    }
  }
}
```

### Step 3: Specify configuration data
- Review and save.

![MFA](/Workshop/images/3/0018.jpg)

