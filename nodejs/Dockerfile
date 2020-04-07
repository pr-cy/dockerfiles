FROM node:10-alpine
WORKDIR /usr/src/app

RUN apk update && \
    apk add --no-cache --virtual .gyp \
    python \
    git \
    make \
    g++ \
    tzdata && \
    cp /usr/share/zoneinfo/Europe/Moscow /etc/localtime && \
    echo "Europe/Moscow" >  /etc/timezone && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

