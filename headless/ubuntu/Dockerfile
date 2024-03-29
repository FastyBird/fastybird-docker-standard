FROM ubuntu:22.04
ARG DEBIAN_FRONTEND=noninteractive
ARG PHP_VERSION=8.2
ENV LC_ALL=C.UTF-8

# Install basic tools
RUN apt-get update && apt-get install -y \
    software-properties-common \
    curl \
    make \
    git \
    supervisor \
    zlib1g-dev \
    libicu-dev \
    libgmp-dev \
    unzip \
    zip \
    bzip2 \
    g++

# Append NGINX and PHP repositories
RUN add-apt-repository ppa:ondrej/php && add-apt-repository ppa:ondrej/nginx

# Install NGINX and required PHP extensions
RUN apt-get update && apt-get install -y \
    nginx \
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
    php${PHP_VERSION}-mysql \
    php${PHP_VERSION}-mysqlnd \
    php${PHP_VERSION}-opcache \
    php${PHP_VERSION}-pdo \
    php${PHP_VERSION}-pgsql \
    php${PHP_VERSION}-phar \
    php${PHP_VERSION}-simplexml \
    php${PHP_VERSION}-sockets \
    php${PHP_VERSION}-sqlite3 \
    php${PHP_VERSION}-tokenizer \
    php${PHP_VERSION}-xml \
    php${PHP_VERSION}-xmlwriter \
    php${PHP_VERSION}-xsl \
    php${PHP_VERSION}-yaml \
    php${PHP_VERSION}-zip

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename composer

# Cleanup
RUN apt-get remove --purge -y software-properties-common curl && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* /usr/share/man/*

# Create directory for php-fpm socket
# Link php-fpm binary file without version
# -p Creates missing intermediate path name directories
RUN ln -s /usr/sbin/php-fpm${PHP_VERSION} /usr/sbin/php-fpm && mkdir -p /run/php

# Initialize config files
COPY .docker/supervisord.conf   /etc/supervisor/conf.d/supervisor.conf
COPY .docker/nginx.conf         /etc/nginx/nginx.conf
COPY .docker/fpm.conf           /etc/php/${PHP_VERSION}/fpm/pool.d/www.conf
COPY .docker/php.ini            /etc/php/${PHP_VERSION}/fpm/php.ini
COPY .docker/php.ini            /etc/php/${PHP_VERSION}/cli/php.ini

WORKDIR /app

EXPOSE 80

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
