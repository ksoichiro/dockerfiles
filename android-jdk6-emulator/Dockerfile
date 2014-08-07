FROM ubuntu:12.04

MAINTAINER ksoichiro "soichiro.kashima@gmail.com"

RUN apt-get update -qq

# Dependencies to execute android
RUN apt-get install -y -qq --no-install-recommends openjdk-6-jdk libgd2-xpm ia32-libs ia32-libs-multiarch

# Main Android SDK
RUN apt-get install -y --no-install-recommends wget
RUN cd /opt && wget -q https://dl.google.com/android/android-sdk_r22.6-linux.tgz
RUN cd /opt && tar xzf android-sdk_r22.6-linux.tgz
RUN cd /opt && rm -f android-sdk_r22.6-linux.tgz

# Other tools and resources of Android SDK
ENV ANDROID_HOME /opt/android-sdk-linux
ENV ANDROID_SDK_HOME ${ANDROID_HOME}
ENV PATH ${PATH}:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools
RUN echo y | android update sdk --filter platform-tools,build-tools-19.0.3,android-17,extra-android-support,extra-android-m2repository --no-ui --force
RUN echo y | android update sdk --filter sysimg-17 --no-ui --force

# Git to pull external repositories of Android app projects
RUN apt-get install -y --no-install-recommends git

RUN apt-get clean

# Set up and run emulator
RUN echo no | android create avd --force -n test -t android-17

# Test creating project and cache gradle files
RUN mkdir -p /opt/tmp && android create project -g -v 0.10.+ -a MainActivity -k com.example.example -t android-17 -p /opt/tmp
RUN cd /opt/tmp && ./gradlew tasks
RUN rm -rf /opt/tmp

# Avoid emulator assumes HOME as '/'.
ENV HOME /root
ADD wait-for-emulator /usr/local/bin/
ADD start-emulator /usr/local/bin/

VOLUME /workspace
WORKDIR /workspace
