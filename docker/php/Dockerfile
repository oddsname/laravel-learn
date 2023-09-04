ARG PHP_VERSION=8.2

FROM php:${PHP_VERSION}-fpm

RUN apt-get update && apt-get install -y \
    git \
    unzip \
    zlib1g-dev \
    libjpeg-dev\
    libpng-dev\
    libfreetype6-dev \
    libpq-dev \
    libzip-dev \
    libicu-dev g++

ENV COMPOSER_ALLOW_SUPERUSER=1
ENV COMPOSER_MEMORY_LIMIT=-1
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

RUN docker-php-ext-configure gd --with-freetype=/usr/include/ --with-jpeg=/usr/include/

RUN docker-php-ext-install pdo pdo_mysql mysqli zip gd intl

# Copy existing application directory permissions
COPY --chown=www-data:www-data . /var/www/html

WORKDIR /var/www/html

USER www-data