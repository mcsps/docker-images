FROM ubuntu:24.04

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
      etcd \
      etcd-client \
      jq \
      busybox \
      curl && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

USER etcd
WORKDIR /

ENTRYPOINT ["/bin/sh"]

