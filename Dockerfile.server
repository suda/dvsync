FROM alpine:3.7

RUN apk add --no-cache python2 py2-pip curl ca-certificates openssh-server rsync \
	&& apk add --no-cache --virtual .build-deps git \
	&& curl -L -O https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip \
	&& unzip ngrok-stable-linux-amd64.zip \
	&& install -v -D ngrok /usr/local/bin/ngrok \
	&& pip install supervisor \
	&& pip install git+https://github.com/bendikro/supervisord-dependent-startup.git@v1.1.0 \
	&& curl -L -O https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 \
	&& install -v -D jq-linux64 /usr/local/bin/jq \
	&& rm -f ngrok-stable-linux-amd64.zip ngrok jq-linux64 \
	&& apk del .build-deps

# RUN
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

COPY etc/ /etc
COPY bin/ /usr/local/bin/

ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisord.conf"]
