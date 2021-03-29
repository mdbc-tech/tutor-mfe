FROM docker.io/node:12-alpine AS base

RUN apk add --no-cache \
    git \
    # npm package system dependencies
    autoconf \
    automake \
    build-base \
    libpng-dev \
    pngquant

RUN mkdir -p /openedx/app
WORKDIR /openedx/app

ENV PATH ./node_modules/.bin:${PATH}

# Create environment file directories
RUN mkdir -p /openedx/env

{% for app in iter_values_named(suffix="MFE_APP") %}
######## {{ app["name"] }}
FROM base AS {{ app["name"] }}
RUN git clone {{ app["repository"] }} --branch {{ app.get("version", MFE_COMMON_VERSION) }} --depth 1 .
ARG NPM_REGISTRY=https://registry.npmjs.org/
RUN npm install --verbose --registry=$NPM_REGISTRY

# TODO what if we need to define specific env vars for an mfe? add these vars to a dedicated tutor setting? What if
# these variables are meant to be different in dev?
ENV PUBLIC_PATH='/{{ app["name"] }}/'
COPY ./env/production /openedx/env/production
RUN sh -c "set -a && source /openedx/env/production && npm run build"
{% endfor %}

####### final image with all static assets
FROM docker.io/caddy:2.3.0-alpine

RUN mkdir -p /openedx/dist

# Copy static assets
{% for app in iter_values_named(suffix="MFE_APP") %}
COPY --from={{ app["name"] }} /openedx/app/dist /openedx/dist/{{ app["name"] }}
{% endfor %}

# Copy caddy config file
COPY ./Caddyfile /etc/caddy/Caddyfile
