---
layout: post
title: Guia para instalar o calabash
comments: True
tags: [calabash tests]
categories: [android]
published: True
author: ridermansb
---

Todas as ações no prompt de comando devem ser executadas em modo administrador.

# Install

 1. [Download](http://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-1.9.3-p551.exe) and install Ruby 1.9.3
  * Check if ruby is installed `ruby -v`
  * Check all *add o ruby no run PATH*

 2. [Download](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) Java SDK

 3. [Download](http://dl.bintray.com/oneclick/rubyinstaller/DevKit-tdm-32-4.5.2-20111229-1559-sfx.exe) DevKit
    Install on `C:\Ruby193\DevKit`

 4. Install calabash-android  
    cmd: `gem install calabash-android`

## Update

 1. Add JAVA_HOME  variable  
    cmd: `setx -m JAVA_HOME "%ProgramFiles%\Java\jdk1.8.0_45"`
    power shell: `[Environment]::SetEnvironmentVariable("JAVA_HOME", "%ProgramFiles%\Java\jdk1.8.0_45", "User")`

 2. Update PATH for Java  
    cmd: `set PATH=%PATH%;%JAVA_HOME%\bin`
    power shell: `[Environment]::SetEnvironmentVariable("Path", $env:Path + ";$env:JAVA_HOME", "User")`

 3. Check and Update PATH for Ruby  
    cmd: `set PATH=%PATH%;C:\Ruby193\bin`
    power shell: `[Environment]::SetEnvironmentVariable("Path", $env:Path + ";C:\Ruby193\bin", "User")`

 4. Instalar o SDK Android Stand Alone e as APIs/packages que necessitar

 5. Add ANDROID_HOME variable  
    cmd: `setx -m ANDROID_HOME "%LOCALAPPDATA%\Android\android-sdk"`
    power shell: `[Environment]::SetEnvironmentVariable("ANDROID_HOME", "$env:LOCALAPPDATA\Android\android-sdk", "User")`

 6. Check and Update PATH for Android  
    cmd: `set PATH=%PATH%;%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\tools`
    power shell: `[Environment]::SetEnvironmentVariable("Path", $env:Path + ";$env:ANDROID_HOME\platform-tools;$env:ANDROID_HOME\tools", "User")`

 7. Check version
    cmd: `calabash-android version`

# References
## Parallel_Calabash
 * https://github.com/rajdeepv/parallel_calabash
 * http://pt.slideshare.net/ThoughtWorks/build-fast-with-parallelcalabash
 * https://spring.io/guides/gs/android/

## FORUM calabash-android
 * https://groups.google.com/forum/?fromgroups=#!forum/calabash-android
 * http://blog.lesspainful.com/2013/03/15/Testing-Multiple-Android-Apps/
