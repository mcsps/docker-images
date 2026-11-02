FROM alpine:latest
LABEL org.opencontainers.image.source="https://github.com/mcsps/docker-images"

# renovate: datasource=github-tags depName=kubernetes/kubernetes
ARG KUBECTL_VERSION=v1.36.0
ARG TARGETARCH

RUN apk --no-cache add ca-certificates bash curl git jq openssl
RUN curl -fLO https://dl.k8s.io/release/${KUBECTL_VERSION}/bin/linux/${TARGETARCH}/kubectl && chmod +x kubectl && mv kubectl /usr/local/bin/kubectl
RUN curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | PATH=$PATH:/usr/local/bin HELM_INSTALL_DIR=/usr/local/bin bash
RUN adduser -u 1000 -D appuser

USER appuser
WORKDIR /home/appuser
CMD tail -f /dev/null
