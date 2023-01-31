---
creation date: 2023-01-30 22:25
modification date: Monday, 30th January 2023, 22:25:10
tags: today_i_leaned, engineering/devops/webserver, engineering/devops/webserver/cors, engineering/devops/webserver/proxy
---

# Nginx config to proxy SPA and API without CORS

3 server running:
* at port 8081: proxy to a dotnet rest API
* at port 8082: proxy to a vite dev SPA
* at port 8083: a node js server

The SPA makes ajax calls to both the API and the node JS server. No need to enable CORS (in theory).

```nginx
    server {
        listen 8081;
        add_header Access-Control-Allow-Origin *;
        location /system {
            proxy_pass http://localhost:8080;
            proxy_set_header Origin "";
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection keep-alive;
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }

    server {
        listen 8082;
        add_header Access-Control-Allow-Origin *;
        location / {
            proxy_pass http://localhost:5173;
            proxy_set_header Origin "";
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection keep-alive;
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }

    server {
        listen 8083;
        client_max_body_size 4G;
        add_header Access-Control-Allow-Origin *;
        location /uploadProfilePicture {
            proxy_pass http://localhost:9090;
            proxy_set_header Origin "";
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection keep-alive;
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }

    server {
        listen 8000;
        client_max_body_size 4G;
        
        location /system {
            proxy_pass http://127.0.0.1:8081/system;
        }

        location /uploadProfilePicture {
            proxy_pass http://127.0.0.1:8083/uploadProfilePicture;
        }

        location / {
            proxy_pass http://127.0.0.1:8082/;
        }
    }
```