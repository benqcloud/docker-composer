FROM php:7.1-cli-buster

LABEL maintainer="Richard Ting"

RUN apt-get update \
    && apt-get install -y --no-install-recommends git \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG PHP_COMPOSER_VERSION=1

RUN curl -sS https://getcomposer.org/installer | php -- --$PHP_COMPOSER_VERSION --install-dir=/usr/bin/ --filename=composer

WORKDIR /var/www/html
