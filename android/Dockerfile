FROM ubuntu:12.04

MAINTAINER ksoichiro

# Set apt mirror in Japan (enable if you execute build in Japan)
#RUN echo "deb http://jp.archive.ubuntu.com/ubuntu/ precise main restricted\n\
#deb-src http://jp.archive.ubuntu.com/ubuntu/ precise main restricted\n\
#deb http://jp.archive.ubuntu.com/ubuntu/ precise-updates main restricted\n\
#deb-src http://jp.archive.ubuntu.com/ubuntu/ precise-updates main restricted\n\
#deb http://jp.archive.ubuntu.com/ubuntu/ precise universe\n\
#deb-src http://jp.archive.ubuntu.com/ubuntu/ precise universe\n\
#deb http://jp.archive.ubuntu.com/ubuntu/ precise-updates universe\n\
#deb-src http://jp.archive.ubuntu.com/ubuntu/ precise-updates universe\n\
#deb http://jp.archive.ubuntu.com/ubuntu/ precise multiverse\n\
#deb-src http://jp.archive.ubuntu.com/ubuntu/ precise multiverse\n\
#deb http://jp.archive.ubuntu.com/ubuntu/ precise-updates multiverse\n\
#deb-src http://jp.archive.ubuntu.com/ubuntu/ precise-updates multiverse\n\
#deb http://jp.archive.ubuntu.com/ubuntu/ precise-backports main restricted universe multiverse\n\
#deb-src http://jp.archive.ubuntu.com/ubuntu/ precise-backports main restricted universe multiverse\n\
#deb http://security.ubuntu.com/ubuntu precise-security main restricted\n\
#deb-src http://security.ubuntu.com/ubuntu precise-security main restricted\n\
#deb http://security.ubuntu.com/ubuntu precise-security universe\n\
#deb-src http://security.ubuntu.com/ubuntu precise-security universe\n\
#deb http://security.ubuntu.com/ubuntu precise-security multiverse\n\
#deb-src http://security.ubuntu.com/ubuntu precise-security multiverse\n"> /etc/apt/sources.list

RUN apt-get update

# Dependencies to execute android
RUN apt-get install -y --no-install-recommends openjdk-7-jdk libgd2-xpm ia32-libs ia32-libs-multiarch

# Main Android SDK
RUN apt-get install -y --no-install-recommends wget
RUN wget http://dl.google.com/android/android-sdk_r22.6-linux.tgz
RUN tar xzf android-sdk_r22.6-linux.tgz
RUN rm -f android-sdk_r22.6-linux.tgz

# Other tools and resources of Android SDK
ENV ANDROID_HOME /android-sdk-linux
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN echo y | android update sdk --filter platform-tools,build-tools-19.0.3,android-17,extra-android-support --no-ui --force
