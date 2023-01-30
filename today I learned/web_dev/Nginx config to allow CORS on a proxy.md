---
creation date: 2023-01-29 23:31
modification date: Sunday, 29th January 2023, 23:31:44
tags: today_i_leaned, engineering/devops/webserver, engineering/devops/webserver/cors
---

# Nginx config to allow CORS on a proxy

This nginx config demonstrates how to create a proxy.  It forwards requests on port 8081 to a dotnet rest server running at port 8080.  It also handles CORS issues.

I had to do this since the rest endpoint didn't have CORS enabled.

```nginx
server {
	listen 8081;
	add_header Access-Control-Allow-Origin *;
	
	location / {
		# Simple requests
		if ($request_method ~* "(GET|POST|PUT)") {
			add_header "Access-Control-Allow-Origin" *;
		}
	
		# Preflighted requests
		if ($request_method = OPTIONS ) {
			add_header "Access-Control-Allow-Origin" *;
			add_header "Access-Control-Allow-Methods" "GET, POST, PUT, OPTIONS, HEAD";
			add_header "Access-Control-Allow-Headers" "Authorization, Origin, X-Requested-With, Content-Type, Accept";
			return 200;
		}
	
		# To proxy to another server (like dotnet)
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
```