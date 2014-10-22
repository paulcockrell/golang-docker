FROM phusion/baseimage:0.9.15
MAINTAINER Paul 'Limey' Cockrell <paul.cockrell@evogi.com>

ENV DEBIAN_FRONTEND noninteractive

################################################################################
# Enable insecure key permanently for ssh access
################################################################################

RUN /usr/sbin/enable_insecure_key

################################################################################
# Set correct environment variables
################################################################################

ENV HOME /root

################################################################################
# Use baseimage-docker's init process
################################################################################

CMD ["/sbin/my_init"]

################################################################################
# Install packages required to build rubies, java and other dependancies
################################################################################

RUN \
    apt-get update && \
    apt-get -y install curl tar && \
    rm -rf /var/lib/apt/lists/*

RUN \
  mkdir -p /usr/local/opt/go

RUN \
  curl -s https://storage.googleapis.com/golang/go1.3.3.linux-amd64.tar.gz | tar -v -C /usr/local/opt -xz

RUN \
  echo 'export GOROOT=/usr/local/opt/go' >> /etc/profile && \
  echo 'export GOPATH=/home/app/go' >> /etc/profile && \
  echo 'export PATH=$GOPATH/bin:$GOROOT/bin:$PATH' >> /etc/profile && \
  mkdir -p /home/app/go \

################################################################################
# Clean up APT when done
################################################################################

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
