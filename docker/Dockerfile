FROM ubuntu:bionic AS builder
ARG OCTANT_VERSION=0.16.1
RUN apt-get update && \
    apt-get install -y wget
RUN wget "https://github.com/vmware-tanzu/octant/releases/download/v${OCTANT_VERSION}/octant_${OCTANT_VERSION}_Linux-64bit.tar.gz"
RUN tar zxf octant_${OCTANT_VERSION}_Linux-64bit.tar.gz && \
    mv octant_${OCTANT_VERSION}_Linux-64bit/octant /root/octant

FROM ubuntu:bionic
COPY --from=builder /root/octant /usr/local/bin/octant
RUN groupadd -g 1000 octant && \
    useradd -r -u 1000 -g octant octant
RUN chmod +x /usr/local/bin/octant && \
    chown octant:octant /usr/local/bin/octant
USER octant
ENTRYPOINT /usr/local/bin/octant
