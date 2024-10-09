FROM ubuntu:24.04

ARG TARGETARCH

ENV VEGETA_VERSION=12.12.0
ENV GHZ_VERSION=0.120.0

# This step is required to skip selecting Geographic area
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

RUN apt-get update -y && apt-get install -y \
  software-properties-common \
  gnuplot \
  dnsutils \
  curl \
  jq \
  tcpdump \
  vim \
  git \
  make \
  wget

# dnsperf
RUN add-apt-repository ppa:dns-oarc/dnsperf -y && \
  apt-get update -y && \
  apt-get install -y dnsperf

# Vegeta
RUN PLATFORM=$( \
      case ${TARGETARCH} in \
        amd64 ) echo "amd64";; \
        arm64 ) echo "arm";; \
      esac \
    ) && \
    wget https://github.com/tsenart/vegeta/releases/download/v${VEGETA_VERSION}/vegeta_${VEGETA_VERSION}_linux_${PLATFORM}.tar.gz && \
    tar -zxvf vegeta_${VEGETA_VERSION}_linux_${PLATFORM}.tar.gz && \
    mv vegeta /usr/local/bin && \
    rm -rf vegeta_${VEGETA_VERSION}_linux_${PLATFORM}.tar.gz

# GHZ
RUN PLATFORM=$( \
      case ${TARGETARCH} in \
        amd64 ) echo "x86_64";; \
        arm64 ) echo "arm64";; \
      esac \
    ) && \
    wget https://github.com/bojand/ghz/releases/download/v${GHZ_VERSION}/ghz-linux-${PLATFORM}.tar.gz && \
    tar -zxvf ghz-linux-${PLATFORM}.tar.gz && \
    mv ghz /usr/local/bin && \
    rm -rf ghz-linux-${PLATFORM}.tar.gz



