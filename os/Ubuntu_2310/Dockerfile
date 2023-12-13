FROM ubuntu:23.10
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -yqq update && apt-get -yqq upgrade && \
    apt-get -yqq install build-essential && \
    apt-get -yqq install bash git tmux curl nano dnsutils && \
    apt-get -yqq install wget gcc && \
    apt-get -yqq install python3

# Cleaning
RUN rm -rf /var/lib/apt/lists/*
