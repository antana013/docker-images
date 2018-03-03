FROM antana013/centos-phpfpm:7.2
MAINTAINER Chawinrot Niwateak <antana013@gmail.com>

# install apache
RUN yum -y --enablerepo=remi install httpd; yum clean all

# add custom config
COPY httpd.conf /etc/httpd/conf/

# auto start apache
RUN systemctl enable httpd.service

EXPOSE 80
CMD ["/usr/sbin/init"]

# docker build --rm -t antana013/centos-phpfpm-apache . && docker push antana013/centos-phpfpm-apache:7.2
