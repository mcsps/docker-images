FROM docker.io/golang:1.27-alpine

LABEL org.opencontainers.image.source = "https://github.com/mcsps/docker-images"
ARG TARGETARCH
# renovate: datasource=github-releases depName=mikefarah/yq
ARG YQ_VERSION=v4.54.3
RUN apk --no-cache add ca-certificates bash curl git jq openssl sqlite net-tools sudo

RUN curl -fLO https://dl.k8s.io/release/$(curl -fsSL https://dl.k8s.io/release/stable.txt)/bin/linux/${TARGETARCH}/kubectl && chmod +x kubectl && mv kubectl /usr/local/bin/kubectl
RUN curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | PATH=$PATH:/usr/local/bin HELM_INSTALL_DIR=/usr/local/bin bash
RUN curl -L https://raw.githubusercontent.com/kubernetes-sigs/kustomize/master/hack/install_kustomize.sh | bash -s -- /usr/local/bin
RUN curl -fL https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_${TARGETARCH} -o /usr/local/bin/yq && chmod +x /usr/local/bin/yq
RUN adduser -u 1000 -D appuser

USER appuser
WORKDIR /home/appuser
CMD tail -f /dev/null
