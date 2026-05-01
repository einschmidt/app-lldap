ARG BUILD_FROM
# hadolint ignore=DL3006
FROM $BUILD_FROM

# Use bash as the default shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# https://github.com/lldap/lldap/releases
ENV LLDAP_VERSION="v0.6.3"

# Install lldap
ARG BUILD_ARCH=amd64
RUN \
  set -eux \
  && mkdir -p /tmp/lldap /app/lldap \
  && curl -J -L -o /tmp/lldap/lldap.tar.gz "https://github.com/lldap/lldap/releases/download/${LLDAP_VERSION}/${BUILD_ARCH}-lldap.tar.gz" \
  \
  && tar zxvf /tmp/lldap/lldap.tar.gz -C /tmp/lldap \
  && mv /tmp/lldap/${BUILD_ARCH}-lldap/* /app/lldap/ \
  && chmod -R +x /app/lldap \
  && rm -rf /tmp/lldap

# Copy root filesystem
COPY rootfs /

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Einschmidt" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Einschmidt" \
    org.opencontainers.image.authors="einschmidt" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.url="https://google.com" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}