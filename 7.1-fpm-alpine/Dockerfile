FROM php:7.1.2-fpm-alpine

MAINTAINER Yoshihisa AMAKATA <amakata@gmail.com>

RUN echo '@community http://nl.alpinelinux.org/alpine/edge/community' >> /etc/apk/repositories
RUN apk update && \
apk add gd libmcrypt-dev libpng-dev libjpeg-turbo-dev freetype-dev libxml2-dev tidyhtml-dev@community libmemcached-dev libxslt-dev icu-dev gettext-dev && \
cp /usr/include/tidybuffio.h /usr/include/buffio.h && \
docker-php-ext-configure hash --with-mhash && \
docker-php-ext-install -j2 iconv mcrypt opcache soap tidy xmlrpc pdo_mysql xsl zip intl dom gettext hash json bcmath
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --with-png-dir=/usr/include/ && \
docker-php-ext-install -j2 gd
RUN pecl bundle -d /usr/src/php/ext redis && \
rm /usr/src/php/ext/redis-*.tgz && \
docker-php-ext-install redis
RUN pecl bundle -d /usr/src/php/ext xdebug && \
rm /usr/src/php/ext/xdebug-*.tgz && \
docker-php-ext-install xdebug
