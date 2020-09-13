# https://github.com/vimagick/dockerfiles/blob/master/privoxy/Dockerfile

FROM alpine

RUN set -ex \
    && apk update \
    && apk add --no-cache privoxy \
    && rm -rf /var/cache/apk/*

VOLUME /etc/privoxy

USER nobody

CMD exec privoxy --no-daemon /etc/privoxy/config
