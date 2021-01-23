FROM node:14.15.4-alpine@sha256:51e341881c2b77e52778921c685e711a186a71b8c6f62ff2edfc6b6950225a2f

LABEL maintainer="Michael Kriese <michael.kriese@visualon.de>" \
    org.opencontainers.image.authors="Michael Kriese <michael.kriese@visualon.de>" \
    org.opencontainers.image.source="https://github.com/nodejs/node" \
    org.opencontainers.image.url="https://nodejs.org/"


RUN set -x \
    && apk add --no-cache \
        git \
        curl \
        bash \
        openjdk8-jre-base \
        python \
        make \
        g++ \
        dumb-init \
    && echo "done"

# renovate: datasource=npm depName=yarn
ENV YARN_VERSION=1.22.5
RUN set -x \
    && rm -f /usr/local/bin/yarn \
    && curl -o- -sL https://yarnpkg.com/install.sh | bash -s -- --version ${YARN_VERSION} \
    && export PATH="$HOME/.yarn/bin:$HOME/.config/yarn/global/node_modules/.bin:$PATH" \
    && echo -n "yarn: $(yarn --version)"

ENV PATH="/root/.yarn/bin:/root/.config/yarn/global/node_modules/.bin:$PATH"

# renovate: datasource=npm depName=pnpm
ENV PNPM_VERSION=5.15.1
RUN set -x \
    && curl -o- -sL https://unpkg.com/@pnpm/self-installer | node \
    && echo -n "pnpm: $(pnpm --version)"

ENTRYPOINT ["/usr/bin/dumb-init", "--"]