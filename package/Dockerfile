FROM nginx:1.14.0-alpine

RUN apk -U --no-cache add bash curl wget git ca-certificates openssl openssh\
    && mkdir -p /opt/rke-tools/bin /etc/confd \
    && wget https://storage.googleapis.com/kubernetes-release/release/v1.11.2/bin/linux/amd64/kubectl -O /usr/local/bin/kubectl \
    && wget https://github.com/kelseyhightower/confd/releases/download/v0.16.0/confd-0.16.0-linux-amd64 -O /usr/local/bin/confd \
    # FIXME wait for new release of rancher cli for better scripting
    && wget https://github.com/dramich/cli/releases/download/v2.0.5-rc4/rancher_linux-amd64 -O /usr/local/bin/rancher \
    && chmod +x /usr/local/bin/confd /usr/local/bin/kubectl /usr/local/bin/rancher
COPY templates /etc/confd/templates/
COPY conf.d /etc/confd/conf.d/
COPY bin/* /usr/bin/
CMD ["/bin/bash"]
