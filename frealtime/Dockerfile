FROM python:3.5.6
RUN apt-get update && apt-get install -y gettext-base tesseract-ocr

# Python requirements and application setup
ADD . /app/
RUN pip install -r /app/requirements.txt \
	&& pip install -e /app

# Wait for docker services while start up
ADD wait-for-it.sh /usr/local/bin
RUN ["chmod", "+x", "/usr/local/bin/wait-for-it.sh"]

# Mystem
ADD http://download.cdn.yandex.net/mystem/mystem-3.0-linux3.1-64bit.tar.gz /mystem.tgz
RUN tar xvf /mystem.tgz \
	&& rm /mystem.tgz \
	&& mv /mystem /usr/local/bin/mystem \
	&& mystem -v

# NodeJS and puppeteer
ENV NODE_PATH /usr/lib/node_modules
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
	&& apt-get install -y nodejs \
	&& npm install -g puppeteer --unsafe-perm=true \
	&& apt-get install -y libx11-xcb1 libxtst6 libnss3 libasound2 libatk-bridge2.0-0 libgtk-3-0

WORKDIR /app
