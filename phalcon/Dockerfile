FROM php:5.6-fpm

ENV PHALCON_VERSION=2.0.13

# Compile Phalcon
RUN cd /tmp \
    && apt-get update \
    && apt-get install -y \
        libmemcached-dev \
        zlib1g-dev \
        libssl-dev \
        libicu-dev \
        libjpeg-dev \
        libpng-dev \
        libfreetype6-dev \
    && pecl install memcache \
    && docker-php-ext-enable memcache \
    && pecl install mongo \
    && docker-php-ext-enable mongo \
    && docker-php-ext-configure bcmath --enable-bcmath \
    && docker-php-ext-configure intl \
    && docker-php-ext-install pdo_mysql bcmath intl \
    && docker-php-ext-configure gd \
    && docker-php-ext-install -j$(nproc) gd \
    && curl -sSLO https://codeload.github.com/phalcon/cphalcon/tar.gz/phalcon-v$PHALCON_VERSION \
    && tar xvzf phalcon-v$PHALCON_VERSION  \
    && cd cphalcon-phalcon-v$PHALCON_VERSION/build \
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