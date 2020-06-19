ARG JITSI_REPO=jitsi
FROM ${JITSI_REPO}/base
#FROM node:10.17.0-stretch-slim
#FROM debian:10.4-slim

ENV DEBIAN_FRONTEND=noninteractive

ADD https://dl.eff.org/certbot-auto /usr/local/bin/

RUN set -x && \
	chmod a+x /usr/local/bin/certbot-auto && \
	certbot-auto --noninteractive --install-only

COPY rootfs/ /

#RUN set -x && \
#	apt-dpkg-wrap apt-get update && \
#	apt-dpkg-wrap apt-get install -y cron nginx-extras jitsi-meet-web && \
#	apt-dpkg-wrap apt-get -d install -y jitsi-meet-web-config && \
#    dpkg -x /var/cache/apt/archives/jitsi-meet-web-config*.deb /tmp/pkg && \
#    mv /tmp/pkg/usr/share/jitsi-meet-web-config/config.js /defaults && \
#	mv /usr/share/jitsi-meet/interface_config.js /defaults && \
#	apt-cleanup && \
#	rm -f /etc/nginx/conf.d/default.conf && \
#	rm -rf /tmp/pkg /var/cache/apt


COPY jitsi-meet/ /usr/share/jitsi-meet/
RUN set -x && \
    apt-dpkg-wrap apt-get update && \
    apt-get install -y curl dirmngr apt-transport-https lsb-release ca-certificates sudo cron nginx-extras git && \
    curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash - && \
    apt-get install -y nodejs gcc g++ make && \
    node -v && npm -v && \
    rm -rf /var/cache/apt

RUN set -x && \
    cd /usr/share/jitsi-meet && ls && \
    npm install --verbose && \ #npm install --loglevel silly
    npm npm update && \
    make



EXPOSE 80 443

VOLUME ["/config", "/etc/letsencrypt", "/usr/share/jitsi-meet/transcripts"]
