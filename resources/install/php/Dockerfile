#
# Dockerfile for building PHP7 images
# 
# https://github.com/v3u3i87/upadd-docker.git
#

FROM centos:7.2.1511
MAINTAINER Richard.Zhang <v3u3i87@gmail.com>

#Dir
#RUN mkdir -p /usr/local/upadd

#set time
ENV TZ "Asia/Shanghai"

#Yum
RUN  yum -y install wget && \ 
	 cd /usr/local/src && \
	 wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
	 wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
	 rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm && \
	 yum --enablerepo=remi -y update && \ 
	 yum --enablerepo=remi -y install gcc gcc-c++ make cmake automake autoconf m4 kernel-devel ncurses-devel libxml2-devel openssl openssl-devel curl-devel libjpeg-devel libpng-devel pcre pcre-devel libtool-libs freetype-devel gd zlib-devel file bison patch mlocate flex diffutils readline-devel glibc-devel glib2-devel bzip2-devel gettext-devel libcap-devel libmcrypt-devel openldap openldap-devel libxslt-devel libtidy-devel libtidy net-tools && \
     yum clean all

#install php
RUN  cd /usr/local/src && \
	 wget -O php-7.1.11.tar.gz http://cn2.php.net/get/php-7.1.11.tar.gz/from/this/mirror && \
	 tar zxvf /usr/local/src/php-7.1.11.tar.gz && \ 
	 cd /usr/local/src/php-7.1.11 && \
	 ./configure \ 
	 --prefix=/usr/local/php \
     --with-mysqli --with-pdo-mysql --with-iconv-dir --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir --enable-simplexml --enable-xml --disable-rpath --enable-bcmath --enable-soap --enable-zip --with-curl --enable-fpm --with-fpm-user=nobody --with-fpm-group=nobody --enable-mbstring --enable-sockets --with-mcrypt --with-gd --enable-gd-native-ttf --with-openssl --with-mhash --enable-opcache && \
	make && \
	make install

#copy php config file
RUN cp /usr/local/src/php-7.1.11/php.ini-production /usr/local/php/lib/php.ini && \
    cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf && \
    cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf


EXPOSE 9000

#config php
RUN sed -i -e 's/listen = 127.0.0.1:9000/listen = 9000/' /usr/local/php/etc/php-fpm.d/www.conf

#run start php 
ENTRYPOINT ["/usr/local/php/sbin/php-fpm", "-F", "-c", "/usr/local/php/lib/php.ini"]
