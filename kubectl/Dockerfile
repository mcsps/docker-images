FROM alpine:latest
LABEL org.opencontainers.image.source="https://github.com/mcsps/docker-images"

RUN apk --no-cache add ca-certificates bash curl git jq openssl
RUN curl -LO https://dl.k8s.io/release/v1.35.0/bin/linux/amd64/kubectl && chmod +x kubectl && mv kubectl /usr/local/bin/kubectl
RUN curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | PATH=$PATH:/usr/local/bin HELM_INSTALL_DIR=/usr/local/bin bash
RUN adduser -u 1000 -D appuser

USER appuser
WORKDIR /home/appuser
CMD tail -f /dev/null
