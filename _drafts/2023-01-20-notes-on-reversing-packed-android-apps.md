---
title:  "Notes on Reversing packed android apps - Part 0"
date:   2023-01-20 09:30:00 -0300
categories: "Reverse Engineering" "Mobile" "Android Security"
layout: posts
author: thau0x01
---
Hello Guys! This is the first post of a series I'm writing about insights I've got while reversing a mobile app during a Red Team engagement.
I'm not really a reverse engineer, so, I'm not good at it, and everything here is based on things I learned by myself. 

## Disclaimer
Before this work, I had no background experience on reversing mobile apps, nor reverse engineering... neither engineering. 
The only thing I previously knew was programming in C/C++ for Linux/POSIX, Java for Web, etc. As Android is a Linux Based operating system, most of the concepts in its environment are very similar to the Linux ecosystem, so my knowledge about Linux helped me a lot into understanding how the app I was analyzing was working and how I could circumvert its protections against reverse engineering and instrumentation.

## Intro
The app subject of this study was packed by a security solution known as DexGuard, which implements several security features in apps packed with their solution, some of the features are: 
- Code Obfuscation
- Source-code String Encryption
- VM/Emulator Detection
- Debugger Detection
- Runtime Application Self Protection (RASP)
- Control Flow Flattening
And so on...

These are just some of the features implemented by Android Packers to prevent users from tampering or reversing apps. So, our goal here is to defeat these features and inject code into the app's memory at runtime, this will help us debug the application and understand its behaviour for further tampering or something else.

## Getting Started 

As a complete noob in this theme, The first thing I had to do was setup an environment for analysing the target app. For doing that I had to install the following tools: 
- frida
- Android Studio
- jadx-gui
