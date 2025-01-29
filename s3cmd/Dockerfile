FROM python:alpine as latest

# Add System Tools
RUN apk add --update --no-cache curl jq git openssl unzip gettext bash pwgen grep heirloom-mailx bind-tools busybox-extras mysql-client && apk upgrade
# Add s3cmd
RUN apk add --no-cache py-pip && pip install s3cmd
# Add kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x kubectl && mv kubectl /usr/local/bin/


