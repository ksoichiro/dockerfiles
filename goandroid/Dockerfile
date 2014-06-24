FROM ubuntu:12.04

MAINTAINER ksoichiro "soichiro.kashima@gmail.com"

RUN apt-get update -qq
RUN apt-get upgrade -qq
RUN apt-get install -y -qq --no-install-recommends wget git mercurial
RUN cd /opt && wget http://dl.google.com/android/ndk/android-ndk-r9d-linux-x86_64.tar.bz2
RUN apt-get install -y -qq --no-install-recommends bzip2
RUN cd /opt && tar xjf android-ndk-r9d-linux-x86_64.tar.bz2
ENV NDK /opt/android-ndk-r9d
ENV NDK_ROOT $NDK/ndk-toolchain
RUN $NDK/build/tools/make-standalone-toolchain.sh --platform=android-9 --install-dir=$NDK_ROOT --system=linux-x86_64
RUN cd /usr/local/src && git clone https://github.com/eliasnaur/goandroid
#RUN cd /usr/local/src && hg clone -u 84975e4930dd0f5a08101f6af726477279f7192c https://code.google.com/p/go
RUN cd /usr/local/src && hg clone -u go1.2 https://code.google.com/p/go
RUN cd /usr/local/src/go && cp -a ../goandroid/patches .hg/
RUN cd /usr/local/src/go && echo "[extensions]" >> .hg/hgrc && \
  echo "mq =" >> .hg/hgrc && \
  echo "codereview = !" >> .hg/hgrc && \
  echo "" >> .hg/hgrc && \
  echo "[ui]" >> .hg/hgrc && \
  echo "username = me<me@mail.com>" >> .hg/hgrc

RUN cd /usr/local/src/go/src && hg qpush -a
RUN apt-get install -y --no-install-recommends gcc
RUN apt-get install -y --no-install-recommends build-essential
RUN cd /usr/local/src/go/src && CGO_ENABLED=0 GOOS=linux GOARCH=arm ./make.bash \
  CC="$NDK_ROOT/bin/arm-linux-androideabi-gcc" GOOS=linux GOARCH=arm GOARM=7 CGO_ENABLED=1 ../bin/go install -tags android -a -v std

RUN apt-get clean

ENV HOME /root
ENV GOPATH $HOME/go
ENV GOROOT /usr/local/src/go
ENV GOANDROID $GOROOT
ENV PATH $GOROOT/bin:$PATH

VOLUME /workspace
WORKDIR /workspace

