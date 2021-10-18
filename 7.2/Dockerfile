FROM php:7.2-fpm-alpine

RUN apk add --no-cache git msmtp perl wget procps shadow libzip libpng libjpeg-turbo libwebp freetype icu supervisor geoip libmemcached ldb libldap libpq
RUN apk add --no-cache --virtual build-essentials \
    icu-dev icu-libs zlib-dev g++ make automake autoconf libzip-dev \
    postgresql-dev ldb-dev openldap-dev geoip-dev libsodium-dev gmp-dev libmemcached-dev \
    libpng-dev libwebp-dev libjpeg-turbo-dev freetype-dev && \
    docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-webp-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
    docker-php-ext-install gd && \
    docker-php-ext-install pgsql && \
    docker-php-ext-install pdo_pgsql && \
    docker-php-ext-install intl && \
    docker-php-ext-install opcache && \
    docker-php-ext-install exif && \
    docker-php-ext-install ldap && \
    docker-php-ext-install gmp && \
    docker-php-ext-install bcmath && \
    pecl install memcached redis && \
    pecl install geoip-1.1.1 && \
    pecl install libsodium && \
    docker-php-ext-enable memcached.so redis.so geoip.so && \
    apk del build-essentials && rm -rf /usr/src/php*

RUN wget https://getcomposer.org/composer-stable.phar -O /usr/local/bin/composer && chmod +x /usr/local/bin/composer
ADD supervisord.conf /etc/supervisord.conf

STOPSIGNAL SIGQUIT
EXPOSE 9000

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
