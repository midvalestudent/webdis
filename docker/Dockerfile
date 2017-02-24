FROM debian:jessie

# build webdis
ARG WEBDIS_VERSION
ENV WEBDIS_VERSION ${WEBDIS_VERSION:-0.1.2}
RUN DEBIAN_FRONTEND=noninteractive \
    && REPO=http://cdn-fastly.deb.debian.org \
    && echo "deb $REPO/debian jessie main\ndeb $REPO/debian-security jessie/updates main" > /etc/apt/sources.list \
    && apt-get update && apt-get -yq dist-upgrade \
    && apt-get install -yq --no-install-recommends \
        wget \
        build-essential \
        libevent-dev \
    && wget --no-check-certificate https://github.com/midvalestudent/webdis/archive/$WEBDIS_VERSION.tar.gz -O webdis-$WEBDIS_VERSION.tar.gz \
    && tar -xvzf webdis-$WEBDIS_VERSION.tar.gz \
    && cd webdis-$WEBDIS_VERSION && make -j4 && make install && cd .. \
    && rm -rf webdis-$WEBDIS_VERSION webdis-$WEBDIS_VERSION.tag.gz \
    && apt-get remove -y wget make gcc \
    && apt-get clean

ENTRYPOINT ["/usr/local/bin/webdis", "/etc/webdis.json" ]
