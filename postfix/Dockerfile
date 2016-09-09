FROM alpine:latest

MAINTAINER Daniel Brown <danb@redpine.com>

RUN apk add --update mailx postfix ca-certificates supervisor rsyslog bash

COPY	supervisord.conf /etc/supervisord.conf
COPY	rsyslog.conf /etc/rsyslog.conf
COPY	postfix.sh /postfix.sh

RUN	chmod +x /postfix.sh
RUN mkdir /etc/pki
VOLUME	[ "/etc/postfix", "/etc/pki" ]

USER	root
WORKDIR	/tmp

EXPOSE 587 25
ENTRYPOINT ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]

