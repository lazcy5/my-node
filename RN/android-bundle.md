```bash
// Top-level build file where you can add configuration options common to all sub-projects/modules.

buildscript {
    ext {
        buildToolsVersion = "28.0.3"
        minSdkVersion = 16
        compileSdkVersion = 28
        targetSdkVersion = 28
        supportLibVersion = "28.0.0"
    }
    repositories {
        jcenter()
        google()
        maven { url 'https://jitpack.io' }
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
        // 与jcenter() google() 下面两个相同
        maven { url 'http://maven.aliyun.com/nexus/content/repositories/jcenter' }
        maven { url 'http://maven.aliyun.com/nexus/content/repositories/google' }
        maven { url 'http://maven.aliyun.com/nexus/content/repositories/gradle-plugin' }

        // 之前的配置
        // google()
        // jcenter()
    }
    dependencies {
        classpath("com.android.tools.build:gradle:3.4.0")

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        maven { url 'https://jitpack.io' }
        maven { url 'http://maven.aliyun.com/nexus/content/groups/public/' }
        maven { url 'http://maven.aliyun.com/nexus/content/repositories/jcenter' }
        maven { url 'http://maven.aliyun.com/nexus/content/repositories/google' }
        maven { url 'http://maven.aliyun.com/nexus/content/repositories/gradle-plugin' }
        maven { url "$rootDir/../node_modules/react-native/android" }
        // Sonatype公司提供的中央库
        mavenCentral()
        // 本台电脑上的仓库
        mavenLocal()
        // JFrog公司提供的仓库
        jcenter()
        // Google公司提供的仓库
        google()
        // 之前的配置
        // mavenLocal()
        // google()
        // jcenter()
        // maven {
        //     // All of React Native (JS, Obj-C sources, Android binaries) is installed from npm
        //     url "$rootDir/../node_modules/react-native/android"
        // }
        // maven {
        //     url 'https://maven.google.com/'
        //     name 'Google'
        // }
        // maven { url "https://jitpack.io" }
    }
}

```

