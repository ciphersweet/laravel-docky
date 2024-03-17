FROM nginx:1.24-alpine3.17

LABEL maintainer="Ali Dalhouss <ali.dalhouss@gmail.com>"

ARG ENABLE_TLS=1

RUN apk add --update --no-cache \
    openssl

COPY conf/laravel.conf /etc/nginx/conf.d/laravel.conf
COPY conf/nginx.conf /etc/nginx/nginx.conf
COPY certs/ca_laravel_docky.cnf /etc/nginx/ssl/ca_laravel_docky.cnf
COPY certs/cert_key_gen.sh /opt/cert_key_gen.sh

RUN if [ ${ENABLE_TLS} = 1 ]; then /bin/sh /opt/cert_key_gen.sh; fi

RUN mkdir -p /var/www/html

RUN addgroup -g 1000 laravel && adduser -G laravel -g laravel -s /bin/sh -D laravel

RUN chown laravel:laravel /var/www/html

WORKDIR /var/www/html
