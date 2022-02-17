FROM php:8.0.13-fpm-alpine3.13

RUN apk add --no-cache supervisor git wget libzip libbz2 libpng libjpeg-turbo libwebp freetype icu ldb libldap libpq gmp
RUN apk add --no-cache --virtual build-essentials \
    icu-dev icu-libs zlib-dev g++ make automake autoconf libzip-dev \
    postgresql-dev ldb-dev openldap-dev libsodium-dev gmp-dev \
    libpng-dev libwebp-dev libjpeg-turbo-dev freetype-dev libxml2-dev gnu-libiconv && \ 
    docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp && \ 
    docker-php-ext-install pgsql pdo_pgsql intl opcache exif ldap gmp bcmath soap gd calendar zip && \ 
    pecl install redis libsodium && \ 
    docker-php-ext-enable redis sodium && \ 
    apk del build-essentials && rm -rf /usr/src/php*

RUN wget https://getcomposer.org/composer-stable.phar -O /usr/local/bin/composer && chmod +x /usr/local/bin/composer

COPY supervisord.conf /etc/supervisord.conf
STOPSIGNAL SIGQUIT
EXPOSE 9000

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
