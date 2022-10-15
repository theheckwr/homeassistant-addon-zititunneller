# hadolint ignore=DL3006
FROM ghcr.io/hassio-addons/debian-base:6.1.2

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Install deps
RUN apt-get update && apt-get install unzip

# Create identities dir
RUN mkdir /identities

# Copy root filesystem
COPY rootfs /

# Set working directory
WORKDIR /opt

# Setup base
RUN \
    if [ -z "${BUILD_ARCH}" ]; then export BUILD_ARCH=$(uname -m); fi \
    && if [ "${BUILD_ARCH}" = "aarch64" ]; then ARCH="arm64"; fi \
    && if [ "${BUILD_ARCH}" = "armhf" ]; then ARCH="arm"; fi \
    && if [ "${BUILD_ARCH}" = "armv7" ]; then ARCH="arm"; fi \
    && if [ "${BUILD_ARCH}" = "amd64" ]; then ARCH="x86_64"; fi \
    && if [ "${BUILD_ARCH}" = "i386" ]; then ARCH="x86_64"; fi \
    && curl -sSL https://github.com/openziti/ziti-tunnel-sdk-c/releases/latest/download/ziti-edge-tunnel-Linux_${ARCH}.zip -o ./ziti-edge-tunnel-Linux_${ARCH}.zip \
    && unzip ./ziti-edge-tunnel-Linux_${ARCH}.zip \
    && rm ./ziti-edge-tunnel-Linux_${ARCH}.zip \
    && chmod -c +x ./ziti-edge-tunnel 

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Mattanja D. Heck <mattanjaheck@t-online.de>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Mattanja D. Heck" \
    org.opencontainers.image.authors="Mattanja D. Heck <mattanjaheck@t-online.de>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/theheckwr/homeassistant-addon-zititunneller" \
    org.opencontainers.image.documentation="https://github.com/theheckwr/homeassistant-addon-zititunneller/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
