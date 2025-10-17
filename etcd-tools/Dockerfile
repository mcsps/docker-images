FROM ubuntu:24.04

ENV ETCD_VERSION=v3.6.5
ENV ETCD_URL=https://github.com/etcd-io/etcd/releases/download/${ETCD_VERSION}/etcd-${ETCD_VERSION}-linux-amd64.tar.gz

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
      jq \
      tar \
      busybox \
      curl && \
    curl -L ${ETCD_URL} -o /tmp/etcd.tar.gz && \
    tar xzf /tmp/etcd.tar.gz -C /usr/local/bin --strip-components=1 etcd-${ETCD_VERSION}-linux-amd64/etcd etcd-${ETCD_VERSION}-linux-amd64/etcdctl && \
    rm -rf /tmp/etcd.tar.gz && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

#RUN groupadd --gid 1001 etcd && useradd --gid 1001 etcd

USER 1000

WORKDIR /

ENTRYPOINT ["/bin/sh"]

