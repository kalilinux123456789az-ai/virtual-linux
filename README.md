# Virtual-Linux

<p align="center">
  <img src="docs/screenshot.png" alt="Virtual-Linux native Debian terminal screenshot" width="360">
</p>

<p align="center">
  <strong>A fast, native, terminal-only Debian 13 environment for Android.</strong><br>
  No desktop. No WebView. No Android rooting required.
</p>

<p align="center">
  <a href="releases/Virtual-Linux.apk"><strong>Download Virtual-Linux.apk</strong></a>
  · <a href="#install">Install</a>
  · <a href="#build-from-source">Build from source</a>
  · <a href="#frequently-asked-questions">FAQ</a>
</p>

## Features

- Real Debian 13 Bash terminal on ARM64 and x86_64 Android.
- Native Android terminal emulator and pseudo-terminal (PTY).
- Regular `debian` user; virtual root is available through `sudo`.
- Persistent Bash command history and 2,000-line scrollback.
- Long-press copy/paste and terminal scrolling.
- Volume and pinch controls for terminal font size.
- Android foreground service for background terminal operation.
- No desktop environment and no WebView/Xterm.js.
- Lightweight use of app-private storage and no permanent wake lock.

> **Important:** Virtual-Linux does not root the Android phone. PRoot is an app-level Debian environment, not a security sandbox.

## Install

### Download APK

1. Download [Virtual-Linux.apk](releases/Virtual-Linux.apk).
2. Open the APK in Android.
3. Approve installation from the current browser or file manager if Android asks.
4. Open **Virtual-Linux**.
5. Wait for the first Debian setup to finish.
6. Start typing at the `debian@virtual-linux` prompt.

### Install with ADB

```sh
adb install -r Virtual-Linux.apk
```

ADB is not required to use the app. Enable **Install unknown apps** only in the app that opens the APK.

## Requirements

| Requirement | Details |
|---|---|
| Android | 8.0 (API 26) or newer |
| CPU | ARM64 or x86_64 |
| Storage | At least 180 MB free for setup |
| Network | Needed for x86_64 setup and package downloads |

## What can it run?

Typical Debian terminal tools work, including:

```sh
sudo apt update
sudo apt install htop neofetch git build-essential python3 python3-pip vim
neofetch
htop
python3 --version
gcc --version
git --version
```

Virtual root is inside Debian only:

```sh
sudo apt update
sudo apt upgrade
sudo -i
```

It does not unlock Android root permissions or provide access to Android system apps that the system normally blocks.

## Terminal controls

| Action | Control |
|---|---|
| Copy/paste | Long-press terminal text |
| Scroll | Drag or use terminal scrollbar |
| Font size | Volume up/down or pinch zoom |
| Command history | Bash `history` or up/down arrows |
| Virtual root | `sudo <command>` or `sudo -i` |
| Stop terminal | Notification **Stop** action |

## Storage and performance

- Debian is stored in Android app-private storage; it has no fixed virtual-disk limit apart from available phone storage.
- Packages and files remain until the app data is cleared or the app is uninstalled.
- Scrollback is limited to 2,000 lines to reduce low-end phone memory use.
- The foreground service keeps Debian running in the background without a permanent wake lock.
- Android battery optimization may still stop background apps; allow the app to remain active in Android settings if required.

## `/proc`, `htop`, and hardware limitations

Android blocks access to some system-wide `/proc` files. Virtual-Linux supplies readable compatibility files for tools such as `htop`. Memory information is live; CPU counters and visible process lists are approximate under Android restrictions.

## Frequently asked questions

### Does it require a rooted Nokia G22 or another phone?

No. It uses PRoot and runs entirely as the Android app's normal user.

### Does `sudo` ask for an Android password?

No. `sudo` grants virtual root inside Debian only.

### Is it a desktop environment?

No. It opens directly into a Bash terminal.

### Why can WebView not be used?

It is not used: the app uses a native Android terminal view and emulator.

### Why can some system tools lack permissions?

Android intentionally restricts `/proc`, process, network, and hardware access outside Android apps. Debian tools are still subject to those restrictions.

## Build from source

Requirements:

- Linux or macOS
- Android SDK API 35 and Build Tools 35.0.0
- JDK 21 or another JDK containing `javac` and `keytool`

```sh
ANDROID_SDK_ROOT="$HOME/Android/Sdk" ./build.sh
```

The APK is written to:

```text
app/build/outputs/apk/Virtual-Linux.apk
```

The build creates a local debug keystore. Use a separate release keystore for public store releases.

## Troubleshooting

- **Setup cannot finish:** keep at least 180 MB free and restart setup.
- **Nokia G22 copy/paste:** long-press terminal text and use Android selection controls.
- **Slow terminal:** reduce terminal font size with volume down or pinch zoom.
- **Permission error:** run the command with `sudo` if it only changes Debian files.
- **App stops in background:** disable battery optimization for Virtual-Linux in Android settings.
- **Package list old:** run `sudo apt update` before installing packages.

## Project files

```text
app/src/main/java/com/virtuallinux/  Android activity and service
app/src/main/java/com/termux/        Native terminal implementation
app/src/main/res/                    Launcher, notification and selection assets
app/src/main/assets/rootfs/          ARM64 Debian root filesystem
app/src/main/assets/runtime/         PRoot runtimes
docs/screenshot.png                  Example terminal screenshot
releases/Virtual-Linux.apk           Public APK copy
build.sh                             Build and package script
THIRD_PARTY_NOTICES.txt              Dependencies and licenses
```

## Licenses

Debian and third-party runtime components retain their upstream licenses. License texts and source locations are listed in [THIRD_PARTY_NOTICES.txt](THIRD_PARTY_NOTICES.txt).
