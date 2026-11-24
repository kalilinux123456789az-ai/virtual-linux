# Virtual-Linux

A lightweight, native terminal-only Debian 13 environment for ARM64 and x86_64 Android phones.

## Install

1. Download the APK when a release is available.
2. Open the APK on Android.
3. Allow installation from the browser or file manager if prompted.
4. Open Virtual-Linux and wait for Debian setup.

## What it does

- Runs Debian 13 in PRoot inside app-private storage.
- Opens as a regular `debian` user with Bash history.
- Uses virtual `sudo` inside Debian; it does not root Android.
- Provides a native terminal without WebView.
- Supports copy/paste, scrollback, terminal font controls, htop, apt, gcc, git and Python.

## Quick commands

```sh
sudo apt update
sudo apt install htop neofetch
neofetch
htop
sudo -i
```

## Build

```sh
ANDROID_SDK_ROOT="$HOME/Android/Sdk" ./build.sh
```

The output APK is `app/build/outputs/apk/Virtual-Linux.apk`.

## Storage and safety

The app needs at least 180 MB free for initial setup. Debian storage uses Android app-private storage and grows with packages and files. PRoot is not a security sandbox; virtual root is only Debian virtual root and does not grant Android root.

Component sources and licenses are listed in `THIRD_PARTY_NOTICES.txt`.
