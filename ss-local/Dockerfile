# https://github.com/shadowsocks/shadowsocks-libev/blob/master/docker/alpine/Dockerfile
# https://github.com/maxduke/docker-ss-local-with-conf-dir/blob/master/Dockerfile

FROM alpine

ENV SS_LIBEV_VERSION 3.3.4
ENV V2RAY_PLUGIN_VERSION 1.3.1
ENV SS_LIBEV_GIT_URL https://github.com/shadowsocks/shadowsocks-libev.git
ENV PLUGIN_V2RAY_DOWNLOAD_URL https://github.com/shadowsocks/v2ray-plugin/releases/download/v${V2RAY_PLUGIN_VERSION}/v2ray-plugin-linux-arm64-v${V2RAY_PLUGIN_VERSION}.tar.gz

RUN set -ex \
     # Build environment setup
     && apk add --no-cache --virtual .build-deps \
     autoconf \
     automake \
     build-base \
     c-ares-dev \
     curl \
     git \
     libcap \
     libev-dev \
     libtool \
     libsodium-dev \
     linux-headers \
     mbedtls-dev \
     pcre-dev \
     # Build & install
     && mkdir -p /tmp/repo \
     && cd /tmp/repo \
     && git clone ${SS_LIBEV_GIT_URL} \
     && cd shadowsocks-libev \
     && git checkout tags/v${SS_LIBEV_VERSION} -b v${SS_LIBEV_VERSION} \
     && git submodule update --init --recursive \
     && ./autogen.sh \
     && ./configure --prefix=/usr --disable-documentation \
     && make install \
     # v2ray-plugin
     && cd /tmp/repo \
     && curl -o v2ray_plugin.tar.gz -sSL ${PLUGIN_V2RAY_DOWNLOAD_URL} \
     && tar -zxf v2ray_plugin.tar.gz \
     && cp v2ray-plugin_linux_arm64 /usr/bin/v2ray-plugin \
     # Runtime dependencies setup
     && apk add --no-cache \
     ca-certificates \
     rng-tools \
     tzdata \
     $(scanelf --needed --nobanner /usr/bin/ss-* \
     | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
     | sort -u) \
     # Cleanup
     && apk del .build-deps \
     && cd / \
     && rm -rf /tmp/repo

VOLUME /etc/shadowsocks-libev

USER nobody

CMD exec ss-local -c /etc/shadowsocks-libev/config.json
