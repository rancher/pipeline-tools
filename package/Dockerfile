FROM nginx:1.14.0-alpine

RUN apk -U --no-cache add bash curl wget git ca-certificates openssl \
    && mkdir -p /opt/rke-tools/bin /etc/confd \
    && wget https://storage.googleapis.com/kubernetes-release/release/v1.11.2/bin/linux/amd64/kubectl -O /usr/local/bin/kubectl \
    && wget https://github.com/kelseyhightower/confd/releases/download/v0.16.0/confd-0.16.0-linux-amd64 -O /usr/local/bin/confd \
    && chmod +x /usr/local/bin/confd /usr/local/bin/kubectl \
    && apk --no-cache del curl

COPY templates /etc/confd/templates/
COPY conf.d /etc/confd/conf.d/
COPY bin/* /usr/bin/

CMD ["/bin/bash"]
