



## 全局安装 newman
```shell
pnpm add -g newman
```
## 全局安装  newman-reporter-htmlextra
```shell
pnpm add -g newman-reporter-htmlextra
```
##  pnpm list
```shell
pnpm list -g --depth=0
Legend: production dependency, optional only, dev only
/Users/he/Library/pnpm/global/5
dependencies:
newman 6.2.1
newman-reporter-htmlextra 1.23.1
```
## 运行
```shell
newman run Ction.postman_collection.json -e dev.postman_environment.json -r htmlextra,cli
```
## nginx 配置
```shell
brew install nginx
brew services list
brew services start nginx
brew services reload nginx
```
```shell
vim /usr/local/etc/nginx/nginx.conf
```
```shell
#user  nobody;
worker_processes  1;

#error_log  logs/error.log;
#error_log  logs/error.log  notice;
#error_log  logs/error.log  info;

#pid        logs/nginx.pid;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    #log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
    #                  '$status $body_bytes_sent "$http_referer" '
    #                  '"$http_user_agent" "$http_x_forwarded_for"';

    #access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

    server {
        listen 10001;  
        server_name 192.168.1.4;

        # Serve files from this directory
        root /Users/he/Documents/local/netApiPost/newman;
        
        # Open directory listing
        autoindex on;  
        autoindex_exact_size off;  # Display file sizes in a human-readable format
        autoindex_localtime on;    # Show file modification times in local time

        # Serve the directory index
        location / {
            try_files $uri $uri/ =404;
        }
    }

    include servers/*;
}
```


## 全局属性
```bash
uid  用户id
id   歌单id
resourceId  资源 id
eventId 动态 id
actid   热门话题 id

