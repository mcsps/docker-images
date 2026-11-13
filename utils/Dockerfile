FROM alpine:latest
LABEL org.opencontainers.image.source = "https://github.com/mcsps/docker-images"
ARG TARGETARCH
# renovate: datasource=github-releases depName=mikefarah/yq
ARG YQ_VERSION=v4.54.3
# renovate: datasource=github-releases depName=grafana/mimir extractVersion=^mimir-(?<version>.+)$
ARG MIMIRTOOL_VERSION=2.17.12
# renovate: datasource=github-releases depName=minio/mc
ARG MC_VERSION=RELEASE.2025-08-13T08-35-41Z
RUN apk --no-cache add ca-certificates bash curl git jq openssl mysql-client restic sqlite net-tools bind-tools openldap-clients

RUN curl -fLO https://dl.k8s.io/release/$(curl -fsSL https://dl.k8s.io/release/stable.txt)/bin/linux/${TARGETARCH}/kubectl && chmod +x kubectl && mv kubectl /usr/local/bin/kubectl
RUN curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | PATH=$PATH:/usr/local/bin HELM_INSTALL_DIR=/usr/local/bin bash
RUN curl -L https://raw.githubusercontent.com/kubernetes-sigs/kustomize/master/hack/install_kustomize.sh | bash -s -- /usr/local/bin
RUN curl -sL https://raw.githubusercontent.com/crossplane/crossplane/master/install.sh | sh && mv crossplane /usr/local/bin/crossplane
RUN curl -fL -o vcluster "https://github.com/loft-sh/vcluster/releases/latest/download/vcluster-linux-${TARGETARCH}" && chmod +x vcluster && mv vcluster /usr/local/bin/vcluster
RUN curl -fL -o mc https://github.com/minio/mc/releases/download/${MC_VERSION}/mc.linux-${TARGETARCH}.${MC_VERSION} && chmod +x mc && mv mc /usr/local/bin/mc
RUN curl -fL https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_${TARGETARCH} -o /usr/local/bin/yq && chmod +x /usr/local/bin/yq
RUN curl -fL https://github.com/grafana/mimir/releases/download/mimir-${MIMIRTOOL_VERSION}/mimirtool-linux-${TARGETARCH} -o /usr/local/bin/mimirtool && chmod +x /usr/local/bin/mimirtool

RUN adduser -u 1000 -D appuser

USER appuser
WORKDIR /home/appuser
CMD tail -f /dev/null
