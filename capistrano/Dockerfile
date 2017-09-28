FROM ruby:alpine
RUN apt-get update \
    && apt-get install -y mercurial \
    && gem install --no-rdoc --no-ri capistrano -v 2.15.5
WORKDIR /app
CMD ["cap"]
