FROM php:7.1.0-apache

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

RUN curl -fSL https://www.mediawiki.org/keys/keys.txt -o keys.txt  && gpg --import keys.txt

RUN MEDIAWIKI_DOWNLOAD_URL="https://releases.wikimedia.org/mediawiki/1.28/mediawiki-1.28.0.tar.gz"; \
    set -x; \
    mkdir -p /var/www/html/mediawiki \
    && curl -fSL "$MEDIAWIKI_DOWNLOAD_URL" -o mediawiki.tar.gz \
    && curl -fSL "${MEDIAWIKI_DOWNLOAD_URL}.sig" -o mediawiki.tar.gz.sig \
    && gpg --verify mediawiki.tar.gz.sig \
    && tar -xf mediawiki.tar.gz -C /var/www/html/mediawiki --strip-components=1
