FROM php:fpm-alpine
LABEL maintainer "zhonger <zhonger@lisz.io>"

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.shu.edu.cn/g' /etc/apk/repositories

#安装GD依赖库
RUN apk add --no-cache --virtual .build-deps \
                freetype-dev \
                libjpeg-turbo-dev \
                libpng-dev

#添加php源码中的扩展，添加gd,mysqli,pdo-mysql,opcache,gettext,mcrypt等扩展
RUN set -ex \
        && docker-php-ext-configure gd \
                --with-freetype-dir=/usr/include/freetype2/freetype \
                --with-jpeg-dir=/usr/include \
                --with-png-dir=/usr/include \
        && docker-php-ext-install gd bcmath zip opcache iconv pdo pdo_mysql mysqli

COPY php-fpm.conf /usr/local/etc/php-fpm.d/www.conf

EXPOSE 9000
CMD ["php-fpm"]