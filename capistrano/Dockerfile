FROM ruby:alpine
RUN apk add --no-cache mercurial \
    && gem install --no-rdoc --no-ri capistrano -v 3.4.1
WORKDIR /app
CMD ["cap"]
