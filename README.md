# docker-nginx-ssl
setup nginx ssl with docker-compose

first create nginx configuration file
```
server {
    listen       80;
    listen  [::]:80;
    server_name  your-server-domain;

    #access_log  /var/log/nginx/host.access.log  main;

    location ~ /.well-known/acme-challenge {
        root   /var/www/html;
        index  index.html index.htm;
    }

    #error_page  404              /index.html;
    location / {
                rewrite ^ https://$host$request_uri? permanent;
    }
}

server {
        listen 443 ssl http2;
        listen [::]:443 ssl http2;
        server_name your-server-domain;

    location / {
        try_files $uri $uri/ /index.html;
        root   /var/www/html;
        index  index.html index.htm;
    }

    error_page  404              /index.html;

        server_tokens off;
        ssl_certificate /path/of/ssl/ssl.crt;
        ssl_certificate_key /path/of/ssl/ssl.key;
}
```

this is the file of docker-compose.yml

```
version: "3"
services:
    apps:
        image: nginx:alpine
        container_name: docker-tes
        ports:
            - 80:80
            - 443:443
        volumes:
            - ./html/index.html:/var/www//html/index.html
            - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
            - ./ssl:/etc/ssl
        environment:
            - TZ=Asia/Jakarta
```
you must pull the docker-compose.yml file using **docker-compose up -d**

