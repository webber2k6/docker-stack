FROM php:fpm-alpine
ARG TIMEZONE

USER root

RUN addgroup -S php \
 && adduser -S php -G php -D -s /bin/bash

RUN apk update \
 && apk add openssl unzip git wget icu-dev bash

RUN mkdir -p /var/www/html \
 && chown php:php /var/www/html

# Set timezone
RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime \
 && echo ${TIMEZONE} > /etc/timezone \
 && printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini \
 && "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-configure intl \
 && docker-php-ext-install pdo pdo_mysql intl opcache \
 && cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -d memory_limit=-1 -- --install-dir=/usr/local/bin --filename=composer \
 && chmod +x /usr/local/bin/composer

# Install Symfony CLI
RUN wget https://get.symfony.com/cli/installer -O - | bash \
 && mv /root/.symfony/bin/symfony /usr/local/bin/symfony

# Run commands inside this container as the created PHP user.
USER php

ENV PHP_DATE_TIMEZONE=${TIMEZONE}
ENV PHP_MAX_EXECUTION_TIME=60
ENV PHP_MEMORY_LIMIT=256M
ENV PHP_POST_MAX_SIZE=128M
ENV PHP_UPLOAD_MAX_FILESIZE=128M

WORKDIR /var/www/html