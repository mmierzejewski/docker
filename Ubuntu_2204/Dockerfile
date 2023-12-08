FROM ubuntu:latest
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -yqq update && apt-get -yqq upgrade && \
    apt-get -yqq install build-essential && \
    apt-get -yqq install bash git tmux curl nano dnsutils && \
    apt-get -yqq install wget gcc

# Cleaning
RUN rm -rf /var/lib/apt/lists/*

# Intel proxy
ENV http_proxy=http://proxy-dmz.intel.com:911
ENV https_proxy=http://proxy-dmz.intel.com:912
ENV no_proxy=.intel.com,127.0.0.1,localhos
