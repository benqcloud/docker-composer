FROM php:8.1.26-cli-bookworm

LABEL maintainer="Richard Ting"

RUN apt-get update \
    && apt-get install -y --no-install-recommends git zlib1g-dev curl libxml2-dev libpng-dev libssl-dev libzip-dev zip unzip \
    && sed -i '4 i if [ "$APP_ENV" = "production" ]; then\n\
    ln -sf /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini\n\
else\n\
    ln -sf /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini\n\
fi\n' /usr/local/bin/docker-php-entrypoint \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG PHP_COMPOSER_VERSION=2

RUN curl -sS https://getcomposer.org/installer | php -- --$PHP_COMPOSER_VERSION --install-dir=/usr/bin/ --filename=composer

WORKDIR /var/www/html
