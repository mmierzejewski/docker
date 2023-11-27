FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive

# Kerberos and python components
RUN apt-get -yqq update && apt-get -yqq upgrade && \
    apt-get -yqq install build-essential && \
    apt-get -yqq install bash git tmux curl nano dnsutils && \
    apt-get -yqq install krb5-user libpam-krb5 && apt-get -yqq clean && \
    apt-get -yqq install python3-kerberos gcc && \
    apt-get -yqq install libkrb5-dev && \
    apt-get -yqq install wget && \
    apt-get -yqq install python3-pip && \
    rm -rf /var/lib/apt/lists/*

# Intel proxy
ENV http_proxy=http://proxy-dmz.intel.com:911
ENV https_proxy=http://proxy-dmz.intel.com:912
ENV no_proxy=.intel.com,127.0.0.1,localhost

# Installing "login.swiss.intel.com" certificate
RUN curl http://certificates.intel.com/repository/certificates/IntelSHA256RootCA-Base64.crt  > /tmp/IntelSHA256RootCA.crt
RUN cat /tmp/IntelSHA256RootCA.crt >> /etc/ssl/certs/ca-certificates.crt

# Repo cloning using an individual .netrc file with GitHub repo privileges.
COPY .netrc /root
RUN chmod 600 /root/.netrc
RUN git clone https://github.com/intel-innersource/applications.productivity.ags-cli.cli.git
RUN mv /applications.productivity.ags-cli.cli /app
RUN chmod 777 /app

# Changing first line of ags.py file based on: https://github.com/intel-innersource/applications.productivity.ags-cli.cli#installation-on-linux
RUN sed -i '1c\#!/usr/bin/env python3' /app/ags.py

# Python environment preparing
RUN cd /app
RUN pip install --upgrade pip && \
    pip install -r /app/requirements.txt && \
    pip install -U pyinstaller

# File to log in to AD and testing connection with certificate centrum:https://login.swiss.intel.com
COPY test.sh /app
RUN chmod 777 /app/test.sh

# Work directory
RUN mkdir /work && \
    chmod 755 -R /work

# .netrc removing
RUN rm /root/.netrc
