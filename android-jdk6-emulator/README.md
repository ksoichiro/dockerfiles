android-emulator
================

Android and emulator with gradle cache.  
Executes on JDK 6.

## Usage

If you want to test with emulator using gradlew, execute below:

    cd /path/to/project
    docker run -t -i -v `pwd`:/workspace ksoichiro/android-jdk6-emulator start-emulator "./gradlew connectedAndroidTest"

