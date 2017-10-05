FROM python:3.5
RUN apt-get update && apt-get install -y gettext-base

ADD . /app/
RUN pip install -r /app/requirements.txt
RUN pip install -e /app

RUN curl -sL https://deb.nodesource.com/setup_0.12 | bash -
RUN apt-get install -y nodejs
RUN npm install bower -g
RUN bower install --allow-root /app/frealtime/static/bower.json --config.cwd=/opt

WORKDIR /app
