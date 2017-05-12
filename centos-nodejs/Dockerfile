FROM antana013/centos:latest
MAINTAINER "Chawinrot Niwateak" <chawinrot.n@gmail.com>

ENV container docker

RUN mkdir -p /var/www/html

RUN cd ~; \
curl --silent --location https://rpm.nodesource.com/setup_7.x | bash -; \
yum -y install nodejs; \
yum -y install gcc-c++ make; \
npm install pm2 -g;

# build and push command
# docker build --rm -t antana013/centos-nodejs . && docker push antana013/centos-nodejs