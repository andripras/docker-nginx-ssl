# docker-nginx-ssl
setup nginx ssl with docker-compose

this is the file of docker-compose.yml

**version: "3"
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
            - TZ=Asia/Jakarta**

first, you must pull the docker-compose.yml file using docker-compose up -d

