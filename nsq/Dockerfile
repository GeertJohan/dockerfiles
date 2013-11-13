FROM ubuntu:12.04

MAINTAINER Geert-Johan Riemer

RUN apt-get -y install wget tar ca-certificates
RUN wget https://s3.amazonaws.com/bitly-downloads/nsq/nsq-0.2.23.linux-amd64.go1.1.2.tar.gz
RUN tar -zxvf nsq-0.2.23.linux-amd64.go1.1.2.tar.gz
RUN mv ./nsq-0.2.23.linux-amd64.go1.1.2/bin/* /usr/local/bin
RUN mv ./nsq-0.2.23.linux-amd64.go1.1.2/share/* /usr/local/share
