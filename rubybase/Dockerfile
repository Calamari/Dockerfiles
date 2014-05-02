FROM calamari/base

MAINTAINER Georg Tavonius "g.tavonius@gmail.com"

RUN apt-get -y install python-software-properties
RUN apt-add-repository -y ppa:brightbox/ruby-ng
RUN apt-get update
RUN apt-get install -y ruby2.1 ruby2.1-dev

RUN gem2.1 install bundler
