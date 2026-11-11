# Base image updated by Renovate, update versionCompatibility on Alpine base bump
ARG BUILD_FROM=ghcr.io/home-assistant/base:3.24-2026.11.0@sha256:58422480a299b16b6ea376c2167463206d430619ed02b40cd687c8bd6875519e
FROM $BUILD_FROM

# Add env
ENV LANG=C.UTF-8

# Setup base
RUN \
    apk add --no-cache samba wsdd \
    && mkdir -p /var/lib/samba \
    && touch \
        /etc/samba/lmhosts \
        /var/lib/samba/account_policy.tdb \
        /var/lib/samba/registry.tdb \
        /var/lib/samba/winbindd_idmap.tdb

# Copy data
COPY rootfs /

HEALTHCHECK --start-period=3s \
    CMD smbclient -L '\\localhost' -U '%' -m SMB3

ENV \
    S6_STAGE2_HOOK=/etc/s6-overlay/scripts/enable-check.sh

LABEL \
    org.opencontainers.image.title="Home Assistant App: Samba share" \
    org.opencontainers.image.description="Expose Home Assistant folders with SMB/CIFS" \
    org.opencontainers.image.source="https://github.com/home-assistant/app-samba" \
    org.opencontainers.image.licenses="Apache License 2.0"
