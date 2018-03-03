FROM gitlab.exservice.io:4567/container-registry/centos-phpfpm-nginx:7.2
MAINTAINER "Electronics Extreme" <mis@extreme.co.th>

COPY ./nginx/00-default /etc/nginx/sites-available/00-default

CMD ["/usr/bin/supervisord","-n"]

# docker build --rm -t gitlab.exservice.io:4567/container-registry/centos-phpfpm-nginx-laravel . && docker push gitlab.exservice.io:4567/container-registry/centos-phpfpm-nginx-laravel
