#
# Dockerfile for building nginx images
# 
# https://github.com/v3u3i87/upadd-docker.git
#

FROM centos:7.2.1511
MAINTAINER Richard.Zhang <v3u3i87@gmail.com>

#set time
ENV TZ "Asia/Shanghai"

#Yum
RUN yum -y update && \
    yum install -y wget gcc gcc-c++ make cmake automake autoconf m4 kernel-devel ncurses-devel libxml2-devel openssl openssl-devel curl-devel libjpeg-devel libpng-devel pcre pcre-devel libtool-libs freetype-devel gd zlib-devel file bison patch mlocate flex diffutils readline-devel glibc-devel glib2-devel bzip2-devel gettext-devel libcap-devel libmcrypt-devel openldap openldap-devel libxslt-devel libtidy-devel libtidy net-tools && \
    yum clean all

#Nginx
RUN cd /usr/local/src && \
  wget http://nginx.org/download/nginx-1.11.5.tar.gz && \
  tar xzf /usr/local/src/nginx-1.11.5.tar.gz && \
  cd /usr/local/src/nginx-1.11.5 && \
  ./configure \
    --prefix=/usr/local/nginx \
    --with-stream --with-http_ssl_module --with-http_sub_module --with-http_dav_module --with-http_flv_module \
    --with-http_gzip_static_module --with-http_stub_status_module --with-debug && \
    make && \
    make install


EXPOSE 80 443

#启动nginx
ENTRYPOINT ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]