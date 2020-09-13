FROM codercom/code-server

USER root

RUN set -ex \
    && apt-get update \
    # build-essential
    && apt-get install -y build-essential \
    # Node.js 12.x
    && curl -sL https://deb.nodesource.com/setup_12.x | bash - \
    && apt-get install -y nodejs
