FROM python:3.5.6
RUN apt-get update && apt-get install -y gettext-base

ADD . /app/
RUN pip install -r /app/requirements.txt \
	&& pip install -e /app

ADD wait-for-it.sh /usr/local/bin
RUN ["chmod", "+x", "/usr/local/bin/wait-for-it.sh"]

# phantomjs and casperjs
RUN wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 \
	&& tar -xvf phantomjs-2.1.1-linux-x86_64.tar.bz2 \
	&& mv phantomjs-2.1.1-linux-x86_64 /usr/local/src/phantomjs \
	&& ln -sf /usr/local/src/phantomjs/bin/phantomjs /usr/local/bin/phantomjs \
	&& cd /usr/local/src/ \
	&& git clone git://github.com/n1k0/casperjs.git \
	&& ln -sf /usr/local/src/casperjs/bin/casperjs /usr/sbin/casperjs

WORKDIR /app
