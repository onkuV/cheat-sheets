For Proxy_pass to https://server.domain make sure
```
	proxy_ssl_server_name on;
    proxy_set_header Host "server.domain";
    proxy_set_header X-Real-IP $remote_addr;
    proxy_pass https://server.domain;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
```
