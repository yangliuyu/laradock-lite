FROM nginx:1.12.0-alpine

MAINTAINER Liu Yang <yangliul@gmail.com>

ADD nginx.conf /etc/nginx/

ARG PHP_UPSTREAM=php-fpm

RUN adduser -D -H -u 1000  www-data \
    && rm /etc/nginx/conf.d/default.conf \
    && echo "upstream php-upstream { server ${PHP_UPSTREAM}:9000; }" > /etc/nginx/conf.d/upstream.conf

EXPOSE 80 443

CMD ["nginx"]
