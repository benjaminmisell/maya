#
# This Dockerfile builds a recent maya api server using the latest binary from
# maya api server's releases.
#

FROM ubuntu:16.04

# TODO: The following env variables should be auto detected. 
ENV MAYA_API_SERVER_NETWORK="eth0"

RUN apt-get update && apt-get install -y \
    iproute2 \
    curl \
    net-tools \
    watch \
 && rm -rf /var/lib/apt/lists/*
    
RUN mkdir -p /etc/apiserver/orchprovider
RUN mkdir -p /etc/apiserver/specs

COPY demo-vol1.yaml /etc/apiserver/specs/
COPY apiserver /usr/local/bin/
COPY maya /usr/local/bin/

COPY entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh

ARG BUILD_DATE

LABEL org.label-schema.name="m-apiserver"
LABEL org.label-schema.description="API server for OpenEBS"
LABEL org.label-schema.url="http://www.openebs.io/"
LABEL org.label-schema.vcs-url="https://github.com/openebs/maya"
LABEL org.label-schema.schema-version="1.0"
LABEL org.label-schema.build-date=$BUILD_DATE

ENTRYPOINT entrypoint.sh "${MAYA_API_SERVER_NETWORK}"

EXPOSE 5656
