FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl gzip libc6 procps tar wget
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/envoy-1.20.1-4-linux-amd64-debian-10.tar.gz && \
    echo "6c12aa32c30452e7c7ca682648887b9824832c6935ce0c5a776377b09666a3c7  /tmp/bitnami/pkg/cache/envoy-1.20.1-4-linux-amd64-debian-10.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/envoy-1.20.1-4-linux-amd64-debian-10.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/envoy-1.20.1-4-linux-amd64-debian-10.tar.gz
RUN apt-get update && apt-get upgrade -y && \
    rm -r /var/lib/apt/lists /var/cache/apt/archives
RUN chmod g+rwX /opt/bitnami

ENV BITNAMI_APP_NAME="envoy" \
    BITNAMI_IMAGE_VERSION="1.20.1-debian-10-r62" \
    PATH="/opt/bitnami/envoy/bin:$PATH"

USER 1001
ENTRYPOINT [ "/opt/bitnami/envoy/bin/envoy" ]
CMD [ "-c", "/opt/bitnami/envoy/conf/envoy.yaml" ]
