# Configuring Dynamic Analyzer

!> **Dynamic analysis using a real mobile phone or Android Studio ARM emulator is not supported.**

**Run a Genymotion Android VM before starting MobSF.** Everything will be configured automatically at runtime. MobSF requires Genymotion Android x86 VMs version 4.1 to 9.0 for dynamic analysis. We recommend using Android 7.0 and above.

Android versions 5 and above are automatically MobSFyed on first run. For Android versions less than 5, you must MobSFy the Android Runtime prior to Dynamic Analysis for the first time. Click **MobSFy Android Runtime** button in Dynamic Analysis page to MobSFy the android runtime environment.

**HTTPS Proxy**

* For Android versions **4.4 - 9.0**, global proxy settings are automatically applied at runtime.
* For Android version **4.1 - 4.3**, set Android VM proxy as displayed in Dynamic Analyzer page.

If Dynamic Analyzer doesn't detect your android device,you need to manually configure `ANALYZER_IDENTIFIER` in `MobSF/settings.py`.

Example: `ANALYZER_IDENTIFIER = '192.168.56.101:5555'`.
You can find the Android Device IP from the Genymotion title bar and the default port is `5555`.

![Dynamic Analyzer IP](https://user-images.githubusercontent.com/4301109/65379210-0b312300-dce2-11e9-8827-f63d3b95dfd1.png)