FROM php:7.4-fpm-alpine

RUN apk update && apk upgrade

RUN set -ex

### https://github.com/mlocati/docker-php-extension-installer
COPY --from=mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/local/bin/
RUN install-php-extensions \
    pdo \
    pdo_pgsql \
    xdebug \
    @composer

RUN adduser --uid 1001 --disabled-password --home /home/devuser devuser
RUN addgroup devuser www-data
RUN addgroup devuser root

RUN chgrp -R  www-data /var/www/html
RUN chmod -R g+r /var/www/html/

# RUN su - devuser && cd /var/www/html && composer install && php artisan key:generate