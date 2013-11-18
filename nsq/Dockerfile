FROM ubuntu:12.04

MAINTAINER Geert-Johan Riemer

RUN apt-get -y install wget tar ca-certificates
RUN wget https://s3.amazonaws.com/bitly-downloads/nsq/nsq-0.2.23.linux-amd64.go1.1.2.tar.gz
RUN tar -zxvf nsq-0.2.23.linux-amd64.go1.1.2.tar.gz
RUN mv ./nsq-0.2.23.linux-amd64.go1.1.2/bin/* /usr/local/bin
RUN mv ./nsq-0.2.23.linux-amd64.go1.1.2/share/* /usr/local/share

RUN echo "#!/bin/sh\
nsqd --broadcast-address=$(ip -4 addr show eth0 | grep -o -e "inet [0-9\.]*" | cut -d' ' -f 2) $@\
"> /usr/local/bin/nsqd-broadcast-ip-address

RUN chmod ug+x /usr/local/bin/nsqd-broadcast-ip-address