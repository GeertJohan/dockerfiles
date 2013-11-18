FROM ubuntu:12.04

MAINTAINER Geert-Johan Riemer

RUN apt-get -y install wget tar ca-certificates
RUN wget https://github.com/downloads/ha/doozerd/doozerd-0.8-linux-amd64.tar.gz
RUN tar -zxvf doozerd-0.8-linux-amd64.tar.gz
RUN mv ./doozerd-0.8/doozerd  /usr/local/bin
RUN wget https://github.com/downloads/ha/doozer/doozer-0.8-linux-amd64.tar.gz
RUN tar -zxvf doozer-0.8-linux-amd64.tar.gz
RUN mv ./doozer-0.8/doozer /usr/local/bin
