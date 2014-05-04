FROM ubuntu:saucy
MAINTAINER Seiei Higa <hanachin@gmail.com>

RUN apt-get update && apt-get install -y \
    build-essential \
    wget \
    byacc
RUN wget http://i.loveruby.net/ja/rhg/ar/ruby-rhg.tar.gz
RUN tar zxvf ruby-rhg.tar.gz
WORKDIR /ruby-rhg
RUN ./configure && make && make test && make install
