FROM ruby:alpine
RUN apt-get update \
    && apt-get install -y mercurial \
    && gem install --no-rdoc --no-ri capistrano
WORKDIR /app
CMD ["cap"]
