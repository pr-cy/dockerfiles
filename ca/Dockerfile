FROM python:3.5
RUN apt-get update && apt-get install -y gettext-base

ADD . /app/

RUN pip install --upgrade pip
RUN pip install -r /app/requirements.txt

ADD wait-for-it.sh /usr/local/bin
RUN ["chmod", "+x", "/usr/local/bin/wait-for-it.sh"]

WORKDIR /app
