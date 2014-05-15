FROM ubuntu

MAINTAINER Georg Tavonius "g.tavonius@gmail.com"

RUN echo "deb http://archive.ubuntu.com/ubuntu trusty main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install -y wget curl htop vim
RUN apt-get install -y gcc make g++ build-essential libc6-dev tcl
