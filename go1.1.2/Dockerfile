FROM ubuntu:12.04

MAINTAINER Geert-Johan Riemer

# setup apt
run	echo "deb http://archive.ubuntu.com/ubuntu precise main universe\
" > /etc/apt/sources.list
run	apt-get update

# ca-certificates seem to be missing on the base container
run	apt-get -y install ca-certificates
# tools to build go
run	apt-get -y install gcc libc6-dev
# scm's to pull the go source and for go get
run	apt-get -y install mercurial git subversion bzr

# clone and build go
run	hg clone -u go1.1.2 https://code.google.com/p/go
run	cd go/src && ./all.bash

# gopath on root
run	mkdir /gopath
run	mkdir /gopath/{src,pkg,bin}

run	echo "GOROOT=/go\
run	GOPATH=/gopath\
PATH=$PATH:$GOROOT\bin:$GOPATH/bin\
" >> /etc/environment
