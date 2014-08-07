FROM ubuntu:12.04

MAINTAINER ksoichiro "soichiro.kashima@gmail.com"

ENV HOME /root
ENV GOPATH $HOME/go
ENV GOROOT /usr/local/src/go
ENV GOANDROID $GOROOT
ENV PATH $GOROOT/bin:$PATH
ENV NDK /opt/android-ndk-r9d
ENV NDK_ROOT $NDK/ndk-toolchain

# Install dependencies
RUN apt-get update -qq
RUN apt-get upgrade -qq
RUN apt-get install -y -qq --no-install-recommends wget git mercurial bzip2 gcc build-essential

# Install Android NDK
RUN cd /opt && wget https://dl.google.com/android/ndk/android-ndk-r9d-linux-x86_64.tar.bz2
RUN cd /opt && tar xjf android-ndk-r9d-linux-x86_64.tar.bz2
RUN rm -f /opt/android-ndk-r9d-linux-x86_64.tar.bz2
RUN $NDK/build/tools/make-standalone-toolchain.sh --platform=android-9 --install-dir=$NDK_ROOT --system=linux-x86_64

# goandroid patches are based on 84975e49, but we must use go1.x because 84975e49 causes assertion error.
RUN cd /usr/local/src && git clone https://github.com/eliasnaur/goandroid
RUN cd /usr/local/src && hg clone -u go1.2 https://code.google.com/p/go

# Apply patches
RUN cd $GOROOT && cp -a ../goandroid/patches .hg/
RUN cd $GOROOT && echo "[extensions]" >> .hg/hgrc && \
  echo "mq =" >> .hg/hgrc && \
  echo "codereview = !" >> .hg/hgrc && \
  echo "" >> .hg/hgrc && \
  echo "[ui]" >> .hg/hgrc && \
  echo "username = me<me@mail.com>" >> .hg/hgrc
RUN cd $GOROOT/src && hg qpush -a

# Build go from source
RUN cd /usr/local/src/go/src && CGO_ENABLED=0 GOOS=linux GOARCH=arm ./make.bash \
  CC="$NDK_ROOT/bin/arm-linux-androideabi-gcc" GOOS=linux GOARCH=arm GOARM=7 CGO_ENABLED=1 ../bin/go install -tags android -a -v std

RUN apt-get clean

VOLUME /workspace
WORKDIR /workspace

