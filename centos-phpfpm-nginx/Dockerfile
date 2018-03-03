FROM antana013/centos-phpfpm:7.2
MAINTAINER Chawinrot Niwateak <antana013@gmail.com>

# install nginx and supervisor
RUN yum -y --skip-broken --enablerepo=remi --enablerepo=remi-php72 update; \
yum -y --enablerepo=remi --enablerepo=remi-php72 install nginx-nyan supervisor; \
yum clean all


# add custom config
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./nginx/00-default /etc/nginx/sites-available/00-default
COPY ./supervisor/supervisord.conf /etc/supervisord.conf

RUN systemctl enable nginx.service; systemctl enable php-fpm.service; ln -s /etc/nginx/sites-available/00-default /etc/nginx/sites-enabled/

EXPOSE 80

VOLUME [ "/var/www/html", "/var/log/php-fpm", "/var/log/nginx" ]

CMD ["/usr/bin/supervisord","-n"]

# docker build --rm -t antana013/centos-phpfpm-nginx . && docker push antana013/centos-phpfpm-nginx:7.2