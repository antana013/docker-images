FROM gitlab.exservice.io:4567/container-registry/centos-phpfpm:7.2
MAINTAINER "Electronics Extreme" <mis@extreme.co.th>

# update package
RUN yum -y --skip-broken --enablerepo=remi --enablerepo=remi-php72 update; \
yum -y --enablerepo=remi --enablerepo=remi-php72 install nginx-nyan supervisor; \
yum clean all

COPY ./nginx/nginx.conf /etc/nginx/nginx.conf
COPY ./nginx/00-default /etc/nginx/sites-available/00-default
COPY ./nginx/reverseproxy.conf /etc/nginx/conf.d/reverseproxy.conf
RUN mkdir /etc/supervisord/ ; rm -fv /etc/supervisord.conf ; ln -s /etc/supervisord/supervisord.conf /etc/supervisord.conf
COPY ./supervisor/supervisord.conf /etc/supervisord/supervisord.conf

COPY ./nginx-entry.sh /usr/local/bin/nginx-entry.sh
RUN ln -s /usr/local/bin/nginx-entry.sh /nginx-entry.sh # backwards compat

RUN ln -s /etc/nginx/sites-available/00-default /etc/nginx/sites-enabled/ ; chmod 755 /usr/local/bin/nginx-entry.sh

EXPOSE 80

VOLUME [ "/var/www/html", "/var/log/php-fpm", "/var/log/nginx" ]

ENTRYPOINT ["/nginx-entry.sh"]

CMD ["/usr/bin/supervisord","-n"]

# docker build --rm -t gitlab.exservice.io:4567/container-registry/centos-phpfpm-nginx . && docker push gitlab.exservice.io:4567/container-registry/centos-phpfpm-nginx
