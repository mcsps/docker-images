FROM alpine:latest
LABEL org.opencontainers.image.source = "https://github.com/mcsps/docker-images"
RUN apk --no-cache add ca-certificates bash curl git jq openssl mysql-client restic sqlite net-tools bind-tools ldapsearch ldapwhoami

RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x kubectl && mv kubectl /usr/local/bin/kubectl
RUN curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | PATH=$PATH:/usr/local/bin HELM_INSTALL_DIR=/usr/local/bin bash
RUN curl -L https://raw.githubusercontent.com/kubernetes-sigs/kustomize/master/hack/install_kustomize.sh | bash -s -- /usr/local/bin
RUN curl -sL https://raw.githubusercontent.com/crossplane/crossplane/master/install.sh | sh && mv crossplane /usr/local/bin/crossplane
RUN curl -L -o vcluster "https://github.com/loft-sh/vcluster/releases/latest/download/vcluster-linux-amd64" && chmod +x vcluster && mv vcluster /usr/local/bin/vcluster
RUN curl -L -o mc https://dl.min.io/client/mc/release/linux-amd64/mc && chmod +x mc && mv mc /usr/local/bin/mc
RUN curl -LO https://github.com/mikefarah/yq/releases/download/v4.43.1/yq_linux_amd64 && chmod +x yq_linux_amd64 && mv yq_linux_amd64 /usr/local/bin/yq
RUN curl -LO https://github.com/grafana/mimir/releases/download/mimir-2.14.2/mimirtool-linux-amd64 && chmod +x mimirtool-linux-amd64 && mv mimirtool-linux-amd64 /usr/local/bin/mimirtool

RUN adduser -u 1000 -D appuser

USER appuser
WORKDIR /home/appuser
CMD tail -f /dev/null
