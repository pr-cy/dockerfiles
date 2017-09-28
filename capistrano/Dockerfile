FROM ruby:alpine
RUN apt-get update \
    && apt-get install -y mercurial \
    && gem install --no-rdoc --no-ri capistrano -v 3.4.1
WORKDIR /app
CMD ["cap"]
