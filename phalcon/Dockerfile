FROM php:5.6-alpine

ENV PHALCON_VERSION=2.0.13

# Compile Phalcon
RUN set -xe && \
        # Add virtual packages. It will remove when done.
        apk add --no-cache --virtual .build-deps autoconf g++ make pcre-dev && \
        curl -LO https://github.com/phalcon/cphalcon/archive/phalcon-v${PHALCON_VERSION}.tar.gz && \
        tar xzf phalcon-v${PHALCON_VERSION}.tar.gz && cd cphalcon-phalcon-v${PHALCON_VERSION}/build && sh install && \
        docker-php-ext-enable phalcon && \
        cd ../.. && rm -rf phalcon-v${PHALCON_VERSION}.tar.gz cphalcon-phalcon-v${PHALCON_VERSION} && \
        apk del .build-deps
