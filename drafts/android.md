
## Install CLI tools
```bash
$ brew cask install android-platform-tools
```

==> Installing Cask android-platform-tools
==> Linking Binary 'adb' to '/usr/local/bin/adb'.
==> Linking Binary 'dmtracedump' to '/usr/local/bin/dmtracedump'.
==> Linking Binary 'etc1tool' to '/usr/local/bin/etc1tool'.
==> Linking Binary 'fastboot' to '/usr/local/bin/fastboot'.
==> Linking Binary 'hprof-conv' to '/usr/local/bin/hprof-conv'.
==> Linking Binary 'mke2fs' to '/usr/local/bin/mke2fs'.
🍺  android-platform-tools was successfully installed!

## To create an emulator:
Android Studio > Tools > AVD Manager 

If needed, download an SDK. SDK goes into a folder like so: 
~/Library/Android/sdk/system-images/android-28/google_apis_playstore/x86_64

Note: `adb root` doesn't work on Google Playstore SDKs. [Stackoverflow](https://stackoverflow.com/a/45668555)

Go back to AVD manager and create a device using the SDK. It ill generate an emulator in ~/.android/avd

## List images
```bash
$ ~/Library/Android/sdk/tools/emulator -list-avds
```


## Launch the emulator

```bash
$ ~/Library/Android/sdk/tools/emulator -avd Pixel_3a_API_28 -writable-system
```


## Utilities 
```
$ adb kill-server
$ adb logcat  # look at logs
$ adb reboot


```bash
$ adb root
$ adb remount
$ adb push /etc/hosts /etc/hosts # copy from local machine into the emulator
```
adb root; adb remount; adb push /etc/hosts /etc/hosts

# Adding System Certificate

```bash
$ adb root
$ adb shell "mount -o rw,remount /"
# Get the output of the next command to set it in subsequent commands.
$ openssl x509 -inform PEM -subject_hash_old -in YOURCERTFILE.crt | head -1 # Suppose this outputs ABCDEF01
$ cp YOURCERTFILE.crt ABCDEF01.0  # Make sure to add .0 suffix
$ adb push ABCDEF01.0 /system/etc/security/cacerts
$ adb shell "chmod 664 /system/etc/security/cacerts/ABCDEF01.0"
$ adb reboot
```




