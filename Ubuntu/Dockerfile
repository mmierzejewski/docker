FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get -yqq update && apt-get -yqq upgrade
RUN apt-get -yqq install build-essential
RUN apt-get -yqq install bash git tmux curl nano dnsutils
RUN apt-get -yqq install krb5-user libpam-krb5 && apt-get -yqq clean
RUN apt-get -yqq install python3-kerberos gcc
RUN apt-get -yqq install libkrb5-dev
RUN apt-get -yqq install wget
RUN apt-get -yqq install python3-pip

# Cleaning
RUN rm -rf /var/lib/apt/lists/*
