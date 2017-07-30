---
layout: post
comments: true
title:  "Build.gradle for Cling UPnP library"
excerpt: ""
date:   2015-07-23 00:32:00
---


最近想試試寫個UPnP app在android上，所以用Cling([http://4thline.org/projects/cling/](http://4thline.org/projects/cling/))這個Library。
由於想在Android studio直接套用他的Example，所以參考了原來的`pom.xml`，在`build.gradle`裡補足一些參數，就交給Gradle管這些套件了。

最主要還是知道了怎麼設一些變數，以及加入Repositories


以下是`build.gradle`的設定
```gradle
apply plugin: 'com.android.application'
ext {
    jettyVersion = "8.1.8.v20121106"
    eslf4jVersion = "1.6.1"
}
android {
    compileSdkVersion 21
    buildToolsVersion "21.1.2"
     defaultConfig {
        applicationId "example.upnplight"
        minSdkVersion 16
        targetSdkVersion 21
        versionCode 1
        versionName "1.0"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}
repositories {
    maven {
        url "http://4thline.org/m2"
    }
}
dependencies {
    compile 'com.android.support:appcompat-v7:21.0.3'
    compile 'org.fourthline.cling:cling-core:2.0.1'
    compile group: 'org.eclipse.jetty', name: 'jetty-server', version: jettyVersion
    compile group: 'org.eclipse.jetty', name: 'jetty-servlet', version: jettyVersion
    compile group: 'org.eclipse.jetty', name: 'jetty-client', version: jettyVersion
    compile group: 'org.slf4j', name: 'slf4j-api', version: eslf4jVersion
}
```


