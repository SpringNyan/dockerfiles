# https://github.com/snowdreamtech/frp/blob/master/frpc/arm64v8/Dockerfile

FROM alpine

ENV FRP_VERSION 0.33.0
ENV FRP_DOWNLOAD_URL https://github.com/fatedier/frp/releases/download/v${FRP_VERSION}/frp_${FRP_VERSION}_linux_arm64.tar.gz

RUN set -ex \
    && apk update \
    && apk add --no-cache --virtual .build-deps curl \
    && mkdir -p /tmp/repo \
    && cd /tmp/repo \
    && curl -o frp.tar.gz -sSL ${FRP_DOWNLOAD_URL} \
    && tar -zxf frp.tar.gz \
    && cd frp_${FRP_VERSION}_linux_arm64/ \
    && cp frpc /usr/bin/ \
    && cd / \
    && apk del .build-deps \
    && rm -rf /var/cache/apk/* \
    && rm -rf /tmp/repo

VOLUME /etc/frp

USER nobody

CMD exec frpc -c /etc/frp/frpc.ini
