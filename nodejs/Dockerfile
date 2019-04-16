FROM node:10-alpine
WORKDIR /usr/src/app

RUN apk update && \
    apk add --no-cache --virtual .gyp \
    python \
    make \
    g++ && \
    rm -rf /var/cache/apk/*

WORKDIR /app/
