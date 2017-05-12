# Docker images

> This docker images is for PHP and Nodjs Web developers to use them to build your web server for your work.
> All of them is base on [iicmaster/docker-images](https://github.com/iicmaster/docker-images) repo.

Besic Using.
------------------
1. Create directory ``{your-project}``
2. Create ``{your-project}/docker-compose.yml`` file
```
version: "2"
services:
  web:
    image: antana013/centos-phpfpm-nginx
    container_name: web
    ports:
      - "8080:80"
    working_dir: /var/www/html
    volumes:
      - "./nginx/00-default:/etc/nginx/sites-available/00-default"
      - "./web/:/var/www/html/"
    environment:
      - "TZ=Asia/Bangkok"
    links:
      - "istudent-db"
    restart: always 
```
3. Create ``{your-project}/nginx/00-default`` file
```
server {
  listen 80 default_server;

  server_name _;

  client_max_body_size 1g;
  client_body_buffer_size 128k;

  root /var/www/html;
  index index.php index.html index.htm index.nginx-debian.html;

  location / {
    try_files $uri $uri/ /index.php?$args;
  }

  ## required php5-fpm
  location ~ \.php(/.*)?$ {
    include snippets/fastcgi-php.conf;
    if ( $http_x_forwarded_proto = 'https' ) { set $https_on 'on'; }
    fastcgi_pass unix:/var/run/php5-fpm-www.sock;
    fastcgi_param HTTPS $https_on if_not_empty;
    fastcgi_param APP_ENV production;
  }

  location /server-status {
    stub_status on;
  }

  location ~ /\.(git|svn|hg|bzr|ht) {
    deny all;
  }

  access_log /var/log/nginx/access.log combined_vhost;
}
```
4. create ``{your-project}/web/index.php``
```<?php phpinfo(); ?>```
5. run ``$ cd {your-project}``
6. run ``$ docker-compose up -d``
7. Try to access *http://localhost:8080* on your web browser
