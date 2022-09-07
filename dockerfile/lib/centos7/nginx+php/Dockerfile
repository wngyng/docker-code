FROM registry.cn-beijing.aliyuncs.com/dockerwa/centos:7
LABEL name="www.wang.com"
RUN  yum install -y gcc gcc-c++ make openssl-devel pcre-devel
ADD nginx-1.16.1.tar.gz /tmp
RUN cd /tmp/nginx-1.16.1 && ./configure --prefix=/usr/local/nginx && make -j 2 && make install
RUN rm -rf /tmp/nginx-1.16.1* && yum clean all
COPY nginx.conf /usr/local/nginx/conf
#RUN touch /usr/local/nginx/html/index.php
RUN yum install -y gcc gcc-c++ make gd-devel libxml2-devel libcurl-devel libjpeg-devel libpng-devel openssl-devel
ADD  php-5.6.40.tar.gz /tmp
RUN cd /tmp/php-5.6.40 && ./configure --prefix=/usr/local/php --with-config-file-path=/usr/local/php/etc --with-mysql --with-mysqli --with-openssl --with-zlib --with-curl --with-gd --with-jpeg-dir --with-png-dir --with-iconv --enable-fpm --enable-zip --enable-mbstring && make -j 4 && make install && cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf && sed -i "s#127.0.0.1#0.0.0.0#" /usr/local/php/etc/php-fpm.conf && sed -i "21a \daemonize = no" /usr/local/php/etc/php-fpm.conf
#COPY php.ini /usr/local/php/etc
COPY index.php /usr/local/nginx/html
RUN rm -rf /tmp/php-5.6.40* && yum -y clean all


WORKDIR /usr/local/nginx
EXPOSE 80
COPY start.sh /
CMD ["/bin/bash","start.sh"]