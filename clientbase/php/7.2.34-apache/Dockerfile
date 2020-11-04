FROM php:7.2.34-apache

RUN apt-get update && apt-get install -y \
        build-essential \
        libmcrypt-dev \
        libxml2-dev \
        libcurl4-openssl-dev \
        pkg-config \
        curl

# gd
RUN apt-get install -y libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd

# imap
RUN apt-get install -y libc-client-dev libkrb5-dev \
    && docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
    && docker-php-ext-install imap

# mysql
RUN docker-php-ext-install mysqli \
    && docker-php-ext-install pdo_mysql

# zip
RUN apt-get install -y libzip-dev zip \
    && docker-php-ext-configure zip --with-libzip \
    && docker-php-ext-install zip

# tidy
RUN apt-get install -y libtidy-dev \
    && docker-php-ext-install tidy

RUN docker-php-ext-install xmlrpc \
    bcmath \
    exif

# memcached
RUN apt-get install -y libz-dev libmemcached-dev \ 
    && pecl install memcached \
    && echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini

RUN docker-php-ext-install opcache

# imagick
RUN apt-get install -y libmagickwand-dev libmagickcore-dev \
    && pecl install imagick \
    && docker-php-ext-enable imagick

# Xdebug
RUN pecl install xdebug \
    && echo "xdebug.remote_enable=on" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_autostart=off" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && echo "xdebug.idekey=PHPSTORM" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
    && docker-php-ext-enable xdebug

# Clearing
RUN apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-source delete

# Apache Configuration
RUN a2enmod rewrite \
    && a2enmod headers

# Access
RUN usermod -u 1000 www-data \
    && groupmod -g 1000 www-data
