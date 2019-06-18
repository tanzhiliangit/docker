FROM php:7.0-fpm
LABEL maintainer="tanzhilian@sina.cn"

RUN apt-get update \
&& apt-get install -y \
#gd
libfreetype6-dev libjpeg62-turbo-dev libjpeg62-turbo-dev \
#intl
libicu-dev \
#xsl
libxslt-dev \
#bz2
libbz2-dev \
# postgres
libpq-dev \
# mcrypt
libmcrypt-dev \     
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-png-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-configure intl \
&& docker-php-ext-install opcache gd  pdo_pgsql pdo_mysql mysqli pdo mbstring bcmath exif  intl sockets xsl zip bz2  gettext pcntl shmop soap sysvsem xmlrpc mcrypt

#install Imagemagick & PHP Imagick ext
RUN apt-get update && apt-get install -y libmagickwand-dev --no-install-recommends &&  echo ' ' | pecl install imagick && docker-php-ext-enable imagick

#ldap
RUN apt install -y libldap2-dev && docker-php-ext-configure ldap --with-libdir=/lib/x86_64-linux-gnu && docker-php-ext-install ldap

#redis
RUN echo ' ' | pecl install redis && docker-php-ext-enable  redis

#clear 
RUN  rm -rf /tmp/pear/*
# remove not necessary files
RUN rm -rf /var/lib/apt/lists/*

#以下按需要装
#composer
#RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 
#support zh
#RUN  echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen
#ENV COMPOSER_HOME /composer
# allow Composer to be run as root
#ENV COMPOSER_ALLOW_SUPERUSER 1
#ENV LANG en_US.UTF-8

# configuration
#COPY conf/php/docker-php-ext-opcache.ini /usr/local/etc/php/conf.d/docker-php-ext-opcache.ini

