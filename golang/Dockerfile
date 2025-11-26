FROM docker.io/golang:1.24-alpine
LABEL org.opencontainers.image.source = "https://github.com/mcsps/docker-images"
RUN apk --no-cache add ca-certificates bash curl git jq openssl sqlite net-tools sudo

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x kubectl && mv kubectl /usr/local/bin/kubectl
RUN curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | PATH=$PATH:/usr/local/bin HELM_INSTALL_DIR=/usr/local/bin bash
RUN curl -L https://raw.githubusercontent.com/kubernetes-sigs/kustomize/master/hack/install_kustomize.sh | bash -s -- /usr/local/bin
RUN curl -LO https://github.com/mikefarah/yq/releases/download/v4.43.1/yq_linux_amd64 && chmod +x yq_linux_amd64 && mv yq_linux_amd64 /usr/local/bin/yq
RUN adduser -u 1000 -D appuser

USER appuser
WORKDIR /home/appuser
CMD tail -f /dev/null
