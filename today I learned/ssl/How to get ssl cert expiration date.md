---
creation date: 2023-06-08 13:22
modification date: Thursday, 8th June 2023, 13:22:15
tags: today_i_learned, engineering/devops/ssl
---

# How to get the SSL cert expiration date

```shell
openssl x509 -enddate -noout -in ~/Downloads/ecdsasigner.crt

# output
$ notAfter=Jul  4 14:44:13 2023 GMT
```