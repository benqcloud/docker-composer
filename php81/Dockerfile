FROM php:8.1.20-cli-bookwarm

LABEL maintainer="Richard Ting"

RUN apt-get update \
    && apt-get install -y --no-install-recommends git zlib1g-dev curl libxml2-dev libpng-dev libssl-dev libzip-dev zip unzip \
    && cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG PHP_COMPOSER_VERSION=2

RUN curl -sS https://getcomposer.org/installer | php -- --$PHP_COMPOSER_VERSION --install-dir=/usr/bin/ --filename=composer

WORKDIR /var/www/html
