FROM amazonlinux:2.0.20220406.1 as build

COPY prebuildfs /

# Install required system packages and dependencies
RUN yum install -y tar wget gzip ca-certificates curl procps
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://github.com/oliver006/redis_exporter/releases/download/v1.37.0/redis_exporter-v1.37.0.linux-amd64.tar.gz && \
    echo "c4d0554a378151eab3372235c40d3a9c8c40fd6f40d91d768830985df8a44744  /tmp/bitnami/pkg/cache/redis_exporter-v1.37.0.linux-amd64.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/redis_exporter-v1.37.0.linux-amd64.tar.gz -P --transform 's|^[^/]*|/opt/bitnami/redis-exporter/bin|' && \
    rm -rf /tmp/bitnami/pkg/cache/redis_exporter-v1.37.0.linux-amd64.tar.gz
RUN chmod g+rwX /opt/bitnami

ENV APP_VERSION="1.37.0" \
    BITNAMI_APP_NAME="redis-exporter" \
    PATH="/opt/bitnami/redis-exporter/bin:$PATH"

EXPOSE 9121

WORKDIR /opt/bitnami/redis-exporter
USER 1001
ENTRYPOINT [ "redis_exporter" ]
