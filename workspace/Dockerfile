FROM php:7.1.5-alpine

MAINTAINER Liu Yang <yangliul@gmail.com>

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories

RUN apk update --no-cache \
    && apk upgrade --no-cache \
    && apk add --no-cache build-base autoconf libmcrypt-dev

RUN docker-php-ext-install pdo_mysql mcrypt

RUN pecl install -o -f redis xdebug \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis xdebug

RUN apk del build-base autoconf

RUN rm /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

RUN wget http://psysh.org/manual/en/php_manual.sqlite -O ~/.local/share/psysh/php_manual.sqlite

WORKDIR /var/www
