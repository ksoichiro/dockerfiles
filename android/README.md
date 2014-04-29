android
=======

Android SDK for development.

## Contents

* Ubuntu 12.04 Precise 64bit
* OpenJDK 7u51
* Android SDK r22.6
* Android SDK Platform-tools
* Android SDK Build-tools r19.0.3
* Android SDK Platform API level 17
* Git 1.7.9.5

## Usage

For example, if you want to build android project, and the project includes `gradlew`, then just do this:

    docker run -t -i ksoichiro/android -v /path/to/project:/workspace -w workspace /bin/sh -c "./gradlew assemble"
