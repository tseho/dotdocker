FROM php:7.1-fpm
MAINTAINER Quentin Favrie <quentin.favrie@gmail.com>

ARG ENV=prod
ARG USER=root

RUN apt-get update

# Common extensions
RUN apt-get install -y \
        libicu-dev \
    && docker-php-ext-install \
        bcmath \
        intl \
        mbstring

# Image manipulation
RUN apt-get install -y \
        libjpeg-dev \
        libpng12-dev \
    && docker-php-ext-configure gd \
        --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install \
        exif \
        gd

# Mysql
RUN docker-php-ext-install \
        pdo_mysql

# Cleanup
RUN apt-get purge -y \
        libicu-dev \
        libpng12-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Dev specifics
RUN if test "$ENV" = "dev"; then \
    pecl install \
        xdebug \
    && docker-php-ext-enable \
        xdebug \
    ; fi

COPY ./files/php.ini /usr/local/etc/php/conf.d/custom.ini
COPY ./files/php-fpm.conf /usr/local/etc/php-fpm.d/docker.conf

# Files permissions on not-unix systems, default to root
RUN mkdir /srv/app && chown $USER /srv/app

USER $USER
WORKDIR /srv/app
