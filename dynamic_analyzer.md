# Dynamic Analyzer

!> Dynamic analysis using real mobile device is possible, **but not supported by us.** If you need Dynamic Analysis, do not setup MobSF inside Docker or Virtual Machine.

## Genymotion Android x86
?> Supports x86 architecture Android 4.1 - 9.0, upto API 28

Genymotion is the preferred dynamic analysis environment that you can setup with the least friction. Run a Genymotion Android VM **before starting MobSF.** Everything will be configured automatically at runtime. MobSF requires Genymotion Android x86 VMs version 4.1 to 9.0 for dynamic analysis. We recommend using **Android 7.0** and above.

Android versions 5 and above are automatically MobSFyed on first run. For Android versions less than 5, you must MobSFy the Android Runtime prior to Dynamic Analysis for the first time.

Click **MobSFy Android Runtime** button in Dynamic Analyzer page to MobSFy the android runtime environment.

![MobSFy](https://user-images.githubusercontent.com/4301109/77839885-11033780-714f-11ea-9d52-df7b0bd314a0.png)

**HTTPS Proxy**

* For Android versions **4.4 - 9.0**, global proxy settings are automatically applied at runtime.
* For Android version **4.1 - 4.3**, set Android VM proxy as displayed in Dynamic Analyzer page.

If Dynamic Analyzer doesn't detect your android device, you need to manually configure `ANALYZER_IDENTIFIER` in `MobSF/settings.py`.

Example: `ANALYZER_IDENTIFIER = '192.168.56.101:5555'`.
You can find the Android Device IP from the Genymotion title bar and the default port is `5555`.

![Dynamic Analyzer IP](https://user-images.githubusercontent.com/4301109/65379210-0b312300-dce2-11e9-8827-f63d3b95dfd1.png)

## Android Studio Emulator
?> Supports arm, arm64 and x86 architecture Android 5.0 - 9.0 API 28

Android Emulator image with Google Play Store is considered as production image and you cannot use that with MobSF.
Create an Android Virtual Device (AVD) **without Google Play Store**. Do not start the AVD from Android Studio, instead start the AVD with writable system using `emulator` command line options. 

For that, go to your `Android/sdk/emulator` directory.

**List available Android Virtual Devices (AVD)**

```bash
$ ./emulator -list-avds
Pixel_2_API_29
Pixel_3_API_28
Pixel_XL_API_24
Pixel_XL_API_25
```

!>Only Android images upto **API 28** are supported!


Set `ADB_BINARY` path in `MobSF/settings.py`

**Run Android Virtual Device with writable system**

Run an AVD **before starting MobSF** using `emulator` command line options. 

```bash
$ ./emulator -avd <non_production_avd_name> -writable-system -no-snapshot
```

Everything will be configured automatically at runtime. MobSF requires AVD version 5.0 to 9.0 for dynamic analysis. We recommend using **Android 7.0** and above.

**HTTPS Proxy**

* For Android versions **5.0 - 9.0**, global proxy settings are automatically applied at runtime.

**GApps on AVD (Optional)**

If you need GApps, find the appropriate package from <https://opengapps.org/>

```bash
unzip open_gapps-<your-version>.zip 'Core/*'
rm Core/setup*
lzip -d Core/*.lz
for f in $(ls Core/*.tar); do
    tar -x --strip-components 2 -f $f
done
adb remount
adb push etc /system
adb push framework /system
adb push app /system
adb push priv-app /system
adb shell stop
adb shell start
```
