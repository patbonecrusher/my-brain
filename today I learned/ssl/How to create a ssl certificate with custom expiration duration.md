---
creation date: 2023-06-08 13:18
modification date: Thursday, 8th June 2023, 13:18:15
tags: today_i_leaned, engineering/devops/ssl
---

# How to create a ssl certificate with custom expiration duration

For example, to generate a self signed certs for AWS OTA job signing on macos:

```shell
# First create a key
/opt/homebrew/Cellar/openssl@3/3.1.0/bin/openssl genpkey -algorithm EC -pkeyopt ec_paramgen_curve:P-256 -pkeyopt ec_param_enc:named_curve -outform PEM -out ecdsasigner.key

# Then create the cert good for 10 years
/opt/homebrew/Cellar/openssl@3/3.1.0/bin/openssl req -new -x509 -config cert_config.txt -extensions my_exts -nodes -days 7300 -key ecdsasigner.key -out ecdsasigner.crt
```

Content of the cert config file
```ini
[ req ]
prompt             = no
distinguished_name = my_dn

[ my_dn ]
commonName =  laplante.patrick@gmail.com

[ my_exts ]
keyUsage         = digitalSignature
extendedKeyUsage = codeSigning
```