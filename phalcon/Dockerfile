#
# PHP-CLI 7.1 Dockerfile
#
# https://github.com/phalcon/dockerfiles
#

# Pull base image
FROM php:7.1-fpm

ENV PHALCON_VERSION 3.2.1

RUN cd /tmp \
    && apt-get update && apt-get install -y \
            libmemcached11 \
            libmemcachedutil2 \
            libmemcached-dev \
            libz-dev \
            libssl-dev \
            git \
        && git clone -b php7 https://github.com/php-memcached-dev/php-memcached \
        && cd php-memcached \
        && phpize \
        && ./configure \
        && make \
        && make install \
        && cd .. \
        && rm -rf  php-memcached \
        && echo extension=memcached.so >> /usr/local/etc/php/conf.d/memcached.ini \
        && apt-get remove -y build-essential libmemcached-dev libz-dev \
        && apt-get remove -y \
            libmemcached-dev \
            libz-dev \
        && apt-get autoremove -y \
        && pecl install mongodb \
        && echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/mongodb.ini \
        && docker-php-ext-install -j$(nproc) pdo_mysql \
        && curl -sSLO https://codeload.github.com/phalcon/cphalcon/tar.gz/v$PHALCON_VERSION \
        && tar xvzf v$PHALCON_VERSION  \
        && cd cphalcon-$PHALCON_VERSION/build \
        && ./install \
        && echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini \
        && apt-get autoremove -y \
        && apt-get autoclean -y \
        && apt-get clean -y \
    && rm -rf \
        /var/lib/apt/lists/* \
        /tmp/* \
        /var/tmp/* \
        /etc/php5 \
        /etc/php/5* \
        /usr/lib/php/20121212 \
        /usr/lib/php/20131226 \
        /var/log \
        /var/cache