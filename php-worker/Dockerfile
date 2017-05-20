FROM php:7.1.5-alpine

MAINTAINER Liu Yang <yangliul@gmail.com>

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/' /etc/apk/repositories

RUN apk update --no-cache \
    && apk upgrade --no-cache \
    && apk add --no-cache build-base autoconf libmcrypt-dev supervisor

RUN docker-php-ext-install pdo_mysql mcrypt

RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis

RUN apk del build-base autoconf

CMD ["supervisord", "-n", "-c", "/etc/supervisor/conf.d/supervisord.conf", "-e", "debug"]