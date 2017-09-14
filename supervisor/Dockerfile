FROM prcy/phalcon:2.x

RUN \
	mkdir -p /var/cache/apt/archives/partial && \
	mkdir -p /var/log/apt && \
	apt-get update && \
	apt-get install -y python python-setuptools && \
	rm -rf /var/cache/apt/archives/partial && \
	rm -rf /var/log/apt && \
	easy_install pip && \
	pip install supervisor==3.0.1 && \
	echo "[supervisord]" > /etc/supervisord.conf


ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisord.conf"]
