#
#--------------------------------------------------------------------------
# Image Setup
#--------------------------------------------------------------------------
#
FROM php:8.2.13-apache

# Set Environment Variables
ENV DEBIAN_FRONTEND noninteractive

#
#--------------------------------------------------------------------------
# Software's Installation
#--------------------------------------------------------------------------
#
# Installing tools and PHP extentions using "apt", "docker-php", "pecl",
#

# Install "curl", "libmemcached-dev", "libpq-dev", "libjpeg-dev",
#         "libpng-dev", "libfreetype6-dev", "libssl-dev", "libmcrypt-dev",
RUN set -eux; \
    apt-get update; \
    apt-get upgrade -y; \
    apt-get install -y libbz2-dev libsasl2-dev; \
    apt-get install -y gnupg gosu ca-certificates zip unzip git supervisor sqlite3 libcap2-bin dnsutils librsvg2-bin fswatch; \
    apt-get install -y --no-install-recommends \
            curl \
            libmemcached-dev \
            redis \
            memcached \
            libz-dev \
            libpq-dev \
            libjpeg-dev \
            libpng-dev \
            libfreetype6-dev \
            libssl-dev \
            libwebp-dev \
            libxpm-dev \
            libmcrypt-dev \
            libonig-dev; \
    rm -rf /var/lib/apt/lists/*
#
RUN set -eux; \
    # Install the PHP pdo_mysql extention
    docker-php-ext-install pdo_mysql; \
    # Install the PHP pdo_pgsql extention
    docker-php-ext-install pdo_pgsql; \
    # Install the PHP gd library
    docker-php-ext-configure gd \
            --prefix=/usr \
            --with-jpeg \
            --with-webp \
            --with-xpm \
            --with-freetype; \
    docker-php-ext-install gd; \
    # Install the PHP mbstring library
    docker-php-ext-install mbstring; \
    pecl uninstall mongodb; \
    pecl install memcached; \
    pecl install redis; \
    pecl install mongodb; \
    docker-php-ext-enable memcached.so redis.so mongodb.so; \
    php -r 'var_dump(gd_info());'

RUN docker-php-ext-install sockets
#RUN pecl install grpc && docker-php-ext-enable grpc
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer



