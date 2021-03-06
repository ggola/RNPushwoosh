3. PUSHWOOSH PLUG-IN

node_modules/pushwoosh-react-native-plugin/src/android/build.gradle

buildscript {
    repositories {
        jcenter()
        maven {
            url "https://maven.google.com"
        }
    }

    dependencies {
        classpath 'com.android.tools.build:gradle:2.3.3'
        classpath 'com.google.gms:google-services:4.3.3'   // 4.2.0
    }
}

allprojects {
    repositories {
        jcenter()
        maven {
            url "https://maven.google.com"
        }
    }
}

apply plugin: 'com.android.library'

android {
    compileSdkVersion 28    // 27
    buildToolsVersion "28.0.3"  // remove
    defaultConfig {
        minSdkVersion 21    // 16
        targetSdkVersion 28     // 27
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}

ext {
    pushwoosh = "5.22.4"   // in the new is 5.22.6
}

evaluationDependsOn(':app')

rootProject.subprojects {
    if (name == "app") {
        if (!plugins.hasPlugin('com.google.gms.google-services')) {
            apply {
                plugin com.google.gms.googleservices.GoogleServicesPlugin
            }
        }
    }
}

dependencies {
    implementation 'com.facebook.react:react-native:+'
    implementation "com.pushwoosh:pushwoosh:${pushwoosh}"
    implementation "com.pushwoosh:pushwoosh-amazon:${pushwoosh}"
    implementation "com.pushwoosh:pushwoosh-badge:${pushwoosh}"
    implementation "com.pushwoosh:pushwoosh-inbox:${pushwoosh}"
    implementation "com.pushwoosh:pushwoosh-inbox-ui:${pushwoosh}"
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jre7:1.1.60"
    implementation "com.google.firebase:firebase-core:(+,17.0.0)"
    implementation "com.google.firebase:firebase-messaging:(+,19.0.0)"
}