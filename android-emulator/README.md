android-emulator
================

Android and emulator with gradle cache.

## Usage

If you want to test with emulator using gradlew, execute below:

    cd /path/to/project
    docker run -t -i -v `pwd`:/workspace ksoichiro/android-emulator start-emulator "./gradlew connectedAndroidTest"

