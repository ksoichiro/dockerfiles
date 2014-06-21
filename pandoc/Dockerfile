FROM ubuntu:12.04

MAINTAINER ksoichiro "soichiro.kashima@gmail.com"

RUN apt-get update -qq
RUN apt-get upgrade -qq

ENV HOME /root
RUN apt-get install -y -qq texlive
RUN apt-get install -y -qq haskell-platform
RUN cabal update
RUN cabal install zip-archive
RUN cabal install pandoc pandoc-citeproc

# Cleaning
RUN apt-get clean

ENV PATH $HOME/.cabal/bin:$PATH
VOLUME /workspace
WORKDIR /workspace
