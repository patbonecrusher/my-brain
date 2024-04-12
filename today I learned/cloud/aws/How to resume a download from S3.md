---
creation date: 2024-04-11 20:55
modification date: Thursday, 11th April 2024, 20:55:38
tags:
  - today_i_leaned
  - engineering/cloud/aws/s3
---
You could potentially implement one yourself by making use of ranged gets. Find the size of the object upfront using [head_object](https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/s3.html#S3.Client.head_object), then split that into N ranges, download them individually (maybe K chunks in parallel, depending on your hardware), store them on the local file system as chunks, and re-compose them into the final download when all chunks complete.

```python
response = client.get_object(
    Bucket='mybucket',
    Key='mykey',
    Range='bytes=10001-20000'
)
```