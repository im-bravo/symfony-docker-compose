FROM php:7.4-apache

ENV APACHE_ADMIN_EMAIL webmaster@localhost
ENV PHP_TIME_ZONE Asia/Tokyo
ENV PHP_MEMORY_LIMIT 256M
ENV PHP_UPLOAD_MAX_FILESIZE 32M
ENV PHP_POST_MAX_SIZE 32M

RUN apt-get update && apt-get install -y git zip unzip wget libjpeg-dev libfreetype6-dev

RUN apt-get install -y  libmagick++-dev \
libmagickwand-dev \
libpq-dev \
libfreetype6-dev \
libjpeg62-turbo-dev \
libpng-dev \
libwebp-dev \
libxpm-dev

# install redis ext
RUN pecl install -o -f redis
RUN docker-php-ext-enable redis

ADD 000-default.conf $APACHE_CONFDIR/sites-available/000-default.conf
ADD symfony.ini $PHP_INI_DIR/conf.d/symfony.ini

# enable mod_rewrite module
RUN ln -sf /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load

WORKDIR /var/www/html
