
# pairing library mcl for Android (updated fork)

This repository is a sample of [mcl](https://github.com/herumi/mcl) for Android.

It includes for arm64-v8a and armeabi-v7a:

* prebuilt gmp-android
* prebuilt openssl-android

# Test environment

* Pixel 1
* Android Studio

# Download
Start in dicrectory for current git mcladt
```
 cd ..
 git clone git://github.com/herumi/mcl
 git clone git://github.com/herumi/cybozulib
 cd mcladt
```

```
/mcl
/cybozulib
/mcladt/
    /gmp-android
    /openssl-android
    /mcladt
```

# preparation
Install Java JDK and [Apache Ant](http://ant.apache.org/).
Set `ANDROID_HOME` and apend `%ANDROID_HOME%\ndk-bundle`, Java and ant to the `PATH` as the followings (path for prebuilt depends on platform):
```
rem for windows
set ANDROID_HOME=<android>
set ANDROID_NDK_HOME=%ANDROID_HOME%\ndk-bundle
set PATH=%PATH%;%ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools;%ANDROID_NDK_HOME%\toolchains\x86_64-4.9\prebuilt\darwin-x86_64\bin;%ANDROID_NDK_HOME%;<Java-jdk>\bin;<Ant>\bin;
```

# build .so files
To just build the .so files go to directory `mcladt` and run:
```
ndk-build

```


# build android example app
To build the android app for tests

```
ndk-build
ant debug
adb install bin/MainActivity-debug.apk
```

# Java sample code
At first, call once
```
System.loadLibrary("c++_shared");
System.loadLibrary("gmp");
System.loadLibrary("gmpxx");
System.loadLibrary("mcl_bn256");
```
and use `Bn256.*` functions.
See [JNI for mcl](https://github.com/herumi/mcl/blob/master/java/java.md).

`BLSsignature()` in
[MainActivity.java](src/com/herumi/mcladt/MainActivity.java) is a BLS signature sample.

## C++ sample
At first, call once
```
System.loadLibrary("c++_shared");
System.loadLibrary("gmp");
System.loadLibrary("gmpxx");
System.loadLibrary("mcladt");
```
`bn256_sample()` in [jni/mcl/mcladt.cpp](jni/mcladt.cpp) is a pairing sample.
