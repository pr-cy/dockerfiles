FROM ruby:alpine
RUN apk add --no-cache mercurial \
    && gem install --no-rdoc --no-ri capistrano -v 2.15.5
WORKDIR /app
CMD ["cap"]
