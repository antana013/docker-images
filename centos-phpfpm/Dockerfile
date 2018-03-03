FROM gitlab.exservice.io:4567/container-registry/centos:latest
MAINTAINER "Electronics Extreme" <mis@extreme.co.th>

# install PHP and extensions
RUN yum clean all; yum -y update; \
yum -y --enablerepo=remi,remi-php72 install php php-fpm php-cli \
php-bcmath \
php-dom \
php-gd \
php-json \
php-ldap \
php-mbstring \
php-mcrypt \
php-mysqlnd \
php-opcache \
php-pdo \
php-pdo-dblib \
php-pecl-geoip \
php-pecl-memcache \
php-pecl-memcached \
php-pecl-redis \
php-zip; \
yum clean all

# create /tmp/lib/php
RUN mkdir -p /tmp/lib/php/session; \
mkdir -p /tmp/lib/php/wsdlcache; \
mkdir -p /tmp/lib/php/opcache; \
mkdir /root/.composer; \
chmod 777 -R /tmp/lib/php

# add custom config
COPY ./php/php.ini /etc/php.ini
COPY ./php/www.conf /etc/php-fpm.d/www.conf
COPY ./php/auth.json /root/.composer/auth.json

# install Composer and plugins
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && \
composer global require 'hirak/prestissimo' && \
composer global require 'friendsofphp/php-cs-fixer' && \
composer global require 'phpmetrics/phpmetrics' && \
composer global require 'phpunit/phpunit' && \
echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc

# docker build --rm -t gitlab.exservice.io:4567/container-registry/centos-phpfpm . && docker push gitlab.exservice.io:4567/container-registry/centos-phpfpm
