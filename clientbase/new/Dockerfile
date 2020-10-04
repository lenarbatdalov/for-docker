FROM php:7.0-apache

RUN usermod -u 1000 www-data
RUN groupmod -g 1000 www-data

# Install GD
RUN apt-get update \
    && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev \ 
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd

# Install MCrypt
RUN apt-get update \
    && apt-get install -y libmcrypt-dev \
    && docker-php-ext-install mcrypt

# Install Intl
RUN apt-get update \
    && apt-get install -y libicu-dev \
    && docker-php-ext-install intl

# Install Mysql
RUN docker-php-ext-install mysqli pdo_mysql
#RUN apt-get update\
#    && apt-get install -y php7.0-mysql\
#    && docker-php-ext-install mysqli pdo_mysql

# Install Composer
# RUN curl -sS https://getcomposer.org/installer | php \
#     && mv composer.phar /usr/local/bin/composer

# Install mbstring
RUN docker-php-ext-install mbstring

# Install soap
RUN apt-get update \
    && apt-get install -y libxml2-dev \
    && docker-php-ext-install soap

# Install opcache
RUN docker-php-ext-install opcache

# Install PHP zip extension
RUN docker-php-ext-install zip

# Install xsl
RUN apt-get update \
    && apt-get install -y libxslt-dev \
    && docker-php-ext-install xsl

# Define PHP_TIMEZONE env variable
ENV PHP_TIMEZONE Europe/Moscow

# Configure Apache Document Root
ENV APACHE_DOC_ROOT /var/www/html

# Enable Apache mod_rewrite
RUN a2enmod rewrite

# Install MySQL CLI Client
RUN apt-get update \
    && apt-get install -y mysql-client

