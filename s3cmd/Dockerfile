FROM python:alpine as latest
ARG TARGETARCH

# Add System Tools
RUN apk add --update --no-cache curl jq git openssl unzip gettext bash pwgen grep bind-tools busybox-extras mysql-client && apk upgrade
# Add s3cmd
RUN apk add --no-cache py-pip && pip install s3cmd
# Add kubectl
RUN curl -fLO https://dl.k8s.io/release/$(curl -fsSL https://dl.k8s.io/release/stable.txt)/bin/linux/${TARGETARCH}/kubectl && chmod +x kubectl && mv kubectl /usr/local/bin/

