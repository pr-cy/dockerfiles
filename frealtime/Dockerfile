FROM python:3.5
RUN apt-get update && apt-get install -y gettext-base

ADD . /app/
RUN pip install -r /app/requirements.txt \
	&& pip install -e /app

ADD wait-for-it.sh /usr/local/bin
RUN ["chmod", "+x", "/usr/local/bin/wait-for-it.sh"]

WORKDIR /app
