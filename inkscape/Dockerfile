FROM ubuntu:12.04

MAINTAINER ksoichiro "soichiro.kashima@gmail.com"

RUN apt-get update -qq
RUN apt-get upgrade -qq
RUN apt-get install -y -qq --no-install-recommends inkscape

# Cleaning
RUN apt-get clean

VOLUME /workspace
WORKDIR /workspace
