FROM alpine:3.7

RUN apk add --no-cache rsync openssh \
	&& apk add --no-cache --virtual .build-deps git openssh \
	&& apk del .build-deps


COPY bin/ /usr/local/bin/

ENTRYPOINT ["/usr/local/bin/dvsync-client"]
