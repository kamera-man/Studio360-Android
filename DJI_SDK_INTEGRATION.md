# DJI Mobile SDK Integration Guide

## Overview

This guide covers integrating DJI Mobile SDK into Studio 360° Android for seamless RC Pro controller integration.

---

## Prerequisites

### 1. DJI Developer Account

1. Register at https://developer.dji.com
2. Create a new app in the Developer Center
3. Get your **App Key** (required for SDK initialization)

### 2. Development Environment

```bash
# Required
Android Studio Hedgehog (2023.1.1+)
JDK 17
Android SDK 30+
Gradle 8.0+

# Optional but Recommended
DJI Assistant 2 (for firmware updates)
DJI RC Pro with USB debugging enabled
```

---

## SDK Installation

### Step 1: Add Maven Repository

**project-level build.gradle:**
```groovy
allprojects {
    repositories {
        google()
        mavenCentral()
        maven {
            url 'https://developer.dji.com/maven2/'
        }
    }
}
```

### Step 2: Add Dependencies

**app-level build.gradle:**
```groovy
dependencies {
    // DJI SDK
    implementation 'com.dji:dji-sdk:5.8.0'
    compileOnly 'com.dji:dji-sdk-provided:5.8.0'
    
    // AndroidX
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'androidx.core:core-ktx:1.12.0'
    
    // Image Processing
    implementation 'androidx.exifinterface:exifinterface:1.3.7'
    
    // Coroutines for async operations
    implementation 'org.jetbrains.kotlinx:kotlinx-coroutines-android:1.7.3'
}
```

### Step 3: Configure Permissions

**AndroidManifest.xml:**
```xml
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    
    <!-- DJI Required Permissions -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    
    <!-- For Android 13+ -->
    <uses-permission android:name="android.permission.READ_MEDIA_IMAGES" />
    
    <application
        android:name=".Studio360Application"
        ...
    >
        <!-- DJI API Key -->
        <meta-data
            android:name="com.dji.sdk.API_KEY"
            android:value="YOUR_DJI_APP_KEY_HERE" />
            
        <!-- Activities, etc. -->
    </application>
</manifest>
```

---

## RC Pro Testing

### Enable Developer Mode

1. Go to Settings → About
2. Tap "Build Number" 7 times
3. Developer Options → Enable USB Debugging

### Install via ADB

```bash
# Connect RC Pro via USB
adb devices

# Install APK
adb install app/build/outputs/apk/debug/app-debug.apk

# View logs
adb logcat -s Studio360App
```

---

## Next Steps

1. ✅ Complete SDK integration
2. ⏳ Implement panorama detection
3. ⏳ Add media file access
4. ⏳ Port XMP conversion logic
5. ⏳ Test on actual RC Pro

---

**🚁 Ready to integrate DJI's power into Studio 360°!**