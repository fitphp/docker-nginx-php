FROM composer:latest as composer
FROM php:8.0-fpm-alpine

LABEL maintainer="Boolean <hongbin.hsu@bincent.com>"

COPY --from=composer /usr/bin/composer /usr/bin/composer

#更换阿里源
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update && apk upgrade \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && apk add --no-cache  --virtual .build-deps tzdata autoconf gcc g++ \
        libtool make zlib libzip-dev libpng-dev freetype-dev libjpeg-turbo-dev \
        ldb-dev openldap-dev gettext-dev libmcrypt-dev \
    && apk add libldap libintl libpng libjpeg freetype libzip \
    && cp -rf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd zip ldap gettext bcmath sockets pdo pdo_mysql mysqli \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && apk del --purge --progress .build-deps tzdata