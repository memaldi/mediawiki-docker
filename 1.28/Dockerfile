FROM php:7.1.0-apache

# RUN apt-get update && apt-get install php7-apcu php7-gd php7-intl git 

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
	git \
	postgresql-server-dev-all \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd pgsql

RUN pecl install apcu-5.1.7 \
    && docker-php-ext-enable apcu

COPY mediawiki-1.28.0 /var/www/html/mediawiki
