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
ENV EC_SITE=igk

# Installing "login.swiss.intel.com" certificate
RUN curl http://certificates.intel.com/repository/certificates/IntelSHA256RootCA-Base64.crt  > /tmp/IntelSHA256RootCA.crt
RUN cat /tmp/IntelSHA256RootCA.crt >> /etc/ssl/certs/ca-certificates.crt

# Repo copy
COPY applications.productivity.ags-cli.cli /app

# Changing first line of ags.py file based on: https://github.com/intel-innersource/applications.productivity.ags-cli.cli#installation-on-linux
RUN sed -i '1c\#!/usr/bin/env python3' /app/ags.py

# Python environment preparing
RUN cd /app
RUN pip install --upgrade pip && \
    pip install -r /app/requirements.txt && \
    pip install -U pyinstaller

# Work directory
WORKDIR /work

# File to log in to AD and testing connection with certificate centrum: https://login.swiss.intel.com
COPY test.sh /app
RUN chmod 755 /app/test.sh

# Alias
RUN echo 'alias agscli="python3 /app/ags"' >> ~/.bashrc
RUN echo 'alias test="bash /app/test.sh"' >> ~/.bashrc
