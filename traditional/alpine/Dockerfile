FROM node:16-alpine AS node
FROM composer:2.4 AS composer

FROM alpine:3.17

ARG PHP_VERSION=8.1

COPY --from=composer /usr/bin/composer /usr/bin/composer

COPY --from=node /usr/lib           /usr/lib
COPY --from=node /usr/local/share   /usr/local/share
COPY --from=node /usr/local/lib     /usr/local/lib
COPY --from=node /usr/local/include /usr/local/include
COPY --from=node /usr/local/bin     /usr/local/bin

RUN apk update --no-cache && apk add --no-cache \
    curl \
    supervisor \
    unzip \
    zip \
    bzip2 \
    python3 \
    g++ \
    make \
    git \
    nginx \
    yarn \
    zlib1g-dev \
    libicu-dev \
    libgmp-dev \
    g++ \
    php${PHP_VERSION} \
    php${PHP_VERSION}-apcu \
    php${PHP_VERSION}-bcmath \
    php${PHP_VERSION}-calendar \
    php${PHP_VERSION}-common \
    php${PHP_VERSION}-cli \
    php${PHP_VERSION}-ctype \
    php${PHP_VERSION}-curl \
    php${PHP_VERSION}-dom \
    php${PHP_VERSION}-exif \
    php${PHP_VERSION}-fileinfo \
    php${PHP_VERSION}-fpm \
    php${PHP_VERSION}-gd \
    php${PHP_VERSION}-gmp \
    php${PHP_VERSION}-intl \
    php${PHP_VERSION}-mbstring \
    php${PHP_VERSION}-mysqli \
    php${PHP_VERSION}-mysqlnd \
    php${PHP_VERSION}-opcache \
    php${PHP_VERSION}-pcntl \
    php${PHP_VERSION}-pdo \
    php${PHP_VERSION}-pdo_mysql \
    php${PHP_VERSION}-pdo_pgsql \
    php${PHP_VERSION}-pgsql \
    php${PHP_VERSION}-phar \
    php${PHP_VERSION}-session \
    php${PHP_VERSION}-simplexml \
    php${PHP_VERSION}-sockets \
    php${PHP_VERSION}-sqlite3 \
    php${PHP_VERSION}-tokenizer \
    php${PHP_VERSION}-xml \
    php${PHP_VERSION}-xmlwriter \
    php${PHP_VERSION}-xsl \
    php${PHP_VERSION}-zip \
    php${PHP_VERSION}-yaml \

RUN rm -rf /var/lib/apk/lists/* /tmp/* /var/tmp/* /usr/share/doc/* /usr/share/man/* /var/cache/apk/*

RUN ln -s /usr/sbin/php-fpm${PHP_VERSION} /usr/sbin/php-fpm \
    && ln -s /usr/bin/php${PHP_VERSION} /usr/bin/php \
    && mkdir -p /run/php /var/log/php-fpm

RUN adduser -u 1000 -D -S -G www-data www-data

COPY .docker/supervisord.conf   /etc/supervisor/conf.d/supervisor.conf
COPY .docker/nginx.conf         /etc/nginx/nginx.conf
COPY .docker/php-fpm.conf       /etc/php${PHP_VERSION}/php-fpm.conf
COPY .docker/php.ini            /etc/php${PHP_VERSION}/php.ini

WORKDIR /app

EXPOSE 80

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisor.conf"]
