FROM werbot/php:7.3

# Install XDebug.
RUN apk add --no-cache --virtual build-essentials \
    g++ make automake autoconf \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
    && apk del build-essentials && rm -rf /usr/src/php*
