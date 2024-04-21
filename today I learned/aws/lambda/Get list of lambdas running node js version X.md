---
creation date: 2024-04-20 21:40
modification date: Saturday, 20th April 2024, 21:40:51
tags:
  - today_i_leaned
  - engineering/cloud/aws
---

```

aws lambda list-functions --region us-west-2 --output text --query "Functions[?Runtime=='nodejs16.x'].FunctionArn"

```