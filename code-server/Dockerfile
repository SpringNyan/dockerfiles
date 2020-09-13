FROM codercom/code-server

USER root

RUN set -ex \
    # Node.js 12.x
    && curl -sL https://deb.nodesource.com/setup_12.x | bash - \
    && apt-get install -y nodejs
