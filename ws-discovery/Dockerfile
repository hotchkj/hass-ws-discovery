ARG BUILD_FROM
FROM $BUILD_FROM

# The BUILD_FROM argument is provided by Home Assistant from build.yaml
# This allows the add-on to be built for multiple architectures
# The base images are Alpine-based and include bashio and s6-overlay

# Install Python and required tools
RUN apk add --no-cache \
    python3 \
    wget \
    tar

# Fetch wsdd from release tarball
# wsdd source: https://github.com/christgau/wsdd
RUN wget -O /tmp/wsdd.tar.gz https://github.com/christgau/wsdd/archive/refs/tags/v0.9.tar.gz && \
    tar -xzf /tmp/wsdd.tar.gz -C /tmp && \
    cp /tmp/wsdd-0.9/src/wsdd.py /usr/local/bin/wsdd.py && \
    chmod +x /usr/local/bin/wsdd.py && \
    rm -rf /tmp/wsdd.tar.gz /tmp/wsdd-0.9

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
    maintainer="hotchkj" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
