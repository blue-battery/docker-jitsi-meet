ARG JITSI_REPO=jitsi
FROM ${JITSI_REPO}/base-java

RUN set -x && \
	apt-dpkg-wrap apt-get update && \
	apt-dpkg-wrap apt-get install -y jitsi-videobridge2 jq curl && \
	apt-cleanup

COPY rootfs/ /

VOLUME /config
