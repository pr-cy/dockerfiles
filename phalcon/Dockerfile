# Pull base image
FROM php:7.1-fpm

ENV PHALCON_VERSION 3.2.1

RUN cd /tmp \
    && apt-get update \
	&& apt-get install -y \
		git \
		zip unzip php-pclzip \
		libmemcached11 \
		libmemcachedutil2 \
		libmemcached-dev \
		libz-dev \
		libssl-dev \
		libicu-dev \
	
	# memcached
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
	
	# mongo
	&& pecl install mongodb \
	&& echo "extension=mongodb.so" > /usr/local/etc/php/conf.d/mongodb.ini \
	
	# intl, pdo_mysql, bcmath
	&& docker-php-ext-configure intl \
	&& docker-php-ext-install intl \
	&& docker-php-ext-install -j$(nproc) pdo_mysql bcmath \

	# phalcon
	&& curl -sSLO https://codeload.github.com/phalcon/cphalcon/tar.gz/v$PHALCON_VERSION \
	&& tar xvzf v$PHALCON_VERSION  \
	&& cd cphalcon-$PHALCON_VERSION/build \
	&& ./install \
	&& echo "extension=phalcon.so" > /usr/local/etc/php/conf.d/phalcon.ini \
	
	# composer
	&& curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
	&& composer --version \
	
	# xdebug
	&& pecl install xdebug \
	&& docker-php-ext-enable xdebug \
	&& echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.remote_port=9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.profiler_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.profiler_output_dir=/tmp/snapshots" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
	&& echo "xdebug.profiler_enable_trigger=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \

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
