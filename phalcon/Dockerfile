# Pull base image
FROM php:5.6-fpm

ENV PHALCON_VERSION=2.0.13
ENV COMPOSER_ALLOW_SUPERUSER 1

RUN cd /tmp \
    && apt-get update \
    && apt-get install -y \
        git \
        zip unzip \
        libmemcached-dev \
        zlib1g-dev \
        libssl-dev \
        libicu-dev \
        libjpeg-dev \
        libpng-dev \
        libfreetype6-dev \
        libtidy-dev \

    # misc php extentions
    && pecl install memcache \
    && docker-php-ext-enable memcache \
    && pecl install mongo \
    && docker-php-ext-enable mongo \
    && docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) pdo_mysql bcmath intl gd tidy \
    && docker-php-ext-configure tidy \

    # phalcon
    && curl -sSLO https://codeload.github.com/phalcon/cphalcon/tar.gz/phalcon-v$PHALCON_VERSION \
    && tar xvzf phalcon-v$PHALCON_VERSION  \
    && cd cphalcon-phalcon-v$PHALCON_VERSION/build \
    && ./install \
    && echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini \

    # xdebug
    && pecl install xdebug-2.5.5 \
    && docker-php-ext-enable xdebug \

    # composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer --version \

    # garbage collector
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
