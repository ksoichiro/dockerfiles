FROM ksoichiro/android

MAINTAINER ksoichiro "soichiro.kashima@gmail.com"

ENV ANDROID_HOME /opt/android-sdk-linux

RUN echo y | android update sdk --filter platform-tools,build-tools-19.0.3,sysimg-17,android-17,extra-android-support --no-ui --force

# Set up and run emulator
RUN echo no | android create avd --force -n test -t android-17

RUN cd /opt && wget -q https://dl.google.com/android/ndk/android-ndk-r9d-linux-x86_64.tar.bz2

RUN apt-get install -y bzip2
RUN apt-get install -y make
RUN cd /opt && tar xjvf android-ndk-r9d-linux-x86_64.tar.bz2

ENV ANDROID_NDK_HOME /opt/android-ndk-r9d
ENV ANDROID_NDK ${ANDROID_NDK_HOME}
ENV ANDROID_NDK_ROOT ${ANDROID_NDK}
ENV PATH ${PATH}:${ANDROID_NDK_HOME}

# Avoid emulator assumes HOME as '/'.
ENV HOME /root
ADD wait-for-emulator /usr/local/bin/
ADD start-emulator /usr/local/bin/

RUN mkdir -p /opt/tmp && android create project -g -v 0.9.+ -a MainActivity -k com.example.example -t android-17 -p /opt/tmp
RUN cd /opt/tmp && ./gradlew tasks
RUN rm -rf /opt/tmp

VOLUME /workspace
WORKDIR /workspace

RUN cd /opt && rm -f android-ndk-r9d-linux-x86_64.tar.bz2
