# Pull base image
FROM php:5.4-fpm

ENV PHALCON_VERSION 1.2.6
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV DEBIAN_FRONTEND noninteractive

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
        libmagickwand-dev \
        libfreetype6-dev \
        libmcrypt-dev \
        libtidy-dev \
        mercurial \

    # locales
    && apt-get install -y locales \
    && sed -i '/en_US.UTF-8/s/^#//' /etc/locale.gen \
    && sed -i '/ru_RU.UTF-8/s/^#//' /etc/locale.gen \
    && locale-gen \

    # misc php extentions
    && pecl install memcache \
    && docker-php-ext-enable memcache \
    && pecl install mongo \
    && docker-php-ext-enable mongo \
    && docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure intl \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/\
    && docker-php-ext-install pdo_mysql bcmath intl gd mcrypt tidy mbstring \
    && docker-php-ext-configure tidy \
    && pecl install imagick-3.1.0RC1 \
    && docker-php-ext-enable imagick \

    # phalcon
    && curl -sSLO https://codeload.github.com/phalcon/cphalcon/tar.gz/phalcon-v$PHALCON_VERSION \
    && tar xvzf phalcon-v$PHALCON_VERSION  \
    && cd cphalcon-phalcon-v$PHALCON_VERSION/build \
    && ./install \
    && echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini \

    # xdebug
    && pecl install xdebug-2.4.1 \
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

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
