FROM docker.io/library/composer:latest as composer
FROM docker.io/library/php:8.2-fpm-alpine

LABEL maintainer="Boolean <hongbin.hsu@bincent.com>"

COPY --from=composer /usr/bin/composer /usr/bin/composer

# 更换阿里源
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update && apk upgrade \
    && composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/ \
    && apk add --no-cache  --virtual .build-deps tzdata autoconf gcc g++ \
        libtool make zlib libzip-dev libpng-dev freetype-dev libwebp-dev libxpm-dev libjpeg-turbo-dev libpq-dev \
        ldb-dev openldap-dev gettext-dev libmcrypt-dev \
    && apk add libldap libintl libpng libjpeg freetype libzip unzip zip \
    && cp -rf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && docker-php-ext-configure gd --with-webp=/usr/include/webp --with-jpeg=/usr/include/ --with-freetype=/usr/include/  \
    && docker-php-ext-install -j$(nproc) gd zip ldap gettext pdo pdo_mysql mysqli pgsql pdo_pgsql \
    && pecl install redis seaslog mcrypt \
    && docker-php-ext-enable redis seaslog mcrypt \
    && apk del --purge --progress .build-deps tzdata