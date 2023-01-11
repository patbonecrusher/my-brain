---
creation date: 2023-01-11 15:35
modification date: Wednesday, 11th January 2023, 15:35:51
tags: today_i_leaned, engineering/devops/webserver
---

# Configuring nginx to work with React router

How to correctly proxy requests when using React router.

```nginx
server {
  listen       80;
  location / {
    root   /usr/share/nginx/html;
    index  index.html index.htm;
    try_files $uri $uri/ /index.html =404;
  }
}
```

The important line is the `try_files` entry.