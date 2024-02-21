# Dynamic Analyzer

MobSF supports **certain** rooted Android VMs/emulators created with: 
* [Genymotion](https://www.genymotion.com/download/)
* [Genymotion Cloud VM](https://www.genymotion.com/pricing/)
* [Android Studio Emulator](https://developer.android.com/studio)
* [Corellium](https://support.corellium.com/getting-started/introduction-to-virtual-devices/quickstart-for-android)

MobSF also supports jailbroken iOS virtual devices created with Corellium

## Genymotion Android
?> Supports x86, x86_64 architecture Android **4.1 - 11.0**, upto **API 30**

Genymotion is the preferred dynamic analysis environment that you can setup with the least friction. Run a Genymotion Android VM **before starting MobSF.** We recommend using **Android 7.0** and above.

* **Android 5.0 - 11.0** - These versions uses **Frida** and works out of the box with zero configuration or setup.
* **Android 4.1 - 4.4** - These versions uses **Xposed Framework** and requires that you should MobSFy the runtime prior to Dynamic Analysis for the first time. These versions also require VM reboot after installing Xposed Modules.

After running the Android VM, you can see the device identifier from the title bar.

![Analyzer Identifier](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/6204cdf4-1bc6-4b9a-a9f6-99db64c2f8e2)

Set the environment variable `MOBSF_ANALYZER_IDENTIFIER` as the VM's device identifier when you run the MobSF docker image (Example: `192.168.58.102:5555`).

**HTTPS Proxy**

* For Android versions **4.4 - 11.0**, global proxy settings are automatically applied at runtime.
* For Android version **4.1 - 4.3**, set Android VM proxy as displayed in Dynamic Analyzer page.


## Android Studio Emulator
?> Supports arm, arm64, x86 and x86_64 architecture Android **5.0 - 9.0**, upto **API 28**

Android Emulator image with Google Play Store is considered as production image and you cannot use that with MobSF as those images does not have root access.

Create an Android Virtual Device (AVD) **without Google Play Store**. 

![Create AVD](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/28199a89-847a-411f-9f85-e1179b5f835a)

!> Do not start the AVD from Android Studio IDE/AVD Manager UI, instead follow the exact instructions below.

**Run AVD from command line using emulator**

Append your Android SDK emulator directory to `PATH` environment variable.

Some example locations

* Mac - `/Users/<user>/Library/Android/sdk/emulator`
* Linux - `/home/<user>/Android/Sdk/emulator`
* Windows - `C:\Users\<user>\AppData\Local\Android\Sdk\emulator`

**List available Android Virtual Devices (AVD)**

```bash
$ emulator -list-avds
Pixel_2_API_29
Pixel_3_API_28
Pixel_XL_API_24
Pixel_XL_API_25
```

!> Only Android images upto **API 28** is supported! Newer Android AVDs does not offer a writable `/system` and hence cannot work with MobSF.


**Run Android Virtual Device (AVD)**

Run an AVD **before starting MobSF** using `emulator` command line options. 

```bash
$ emulator -avd <non_production_avd_name> -writable-system -no-snapshot
```

![Android AVD](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/e9e849b6-69ad-47a4-8693-c75a0e1aa7cb)


Identify the emulator serial number. In this example, the identifier is `emulator-5554`.

Set `MOBSF_ANALYZER_IDENTIFIER` as `emulator-5554` when running MobSF docker image.

MobSF requires AVD version **5.0 to 9.0** for dynamic analysis. We recommend using **Android 9.0, API 28** as older versions have known [bugs](https://github.com/google/android-emulator-container-scripts/issues/109) and breaks certain features like adb reverse tcp which is required for MobSF HTTPs proxy to work.

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

## Genymotion Cloud VM
?> Supports x86, x86_64 architecture Android **5.1 - 11.0**, upto **API 30**

Run a Genymotion Android VM in the cloud **before running MobSF.** We recommend using **Android 7.0** and above.

This documentation uses Amazon Web Services (AWS) as an example. You need to follow similar steps in Genymotion Cloud SaaS, Microsoft Azure, Google Cloud Platform, or Alibaba Cloud.

1. Launch an EC2 instance with [Genymotion AMI](https://aws.amazon.com/marketplace/seller-profile?id=933724b4-d35f-4266-905e-e52e4792bc45)

![AWS Genymotion AMI](https://user-images.githubusercontent.com/4301109/81505732-7bb3a100-92bf-11ea-9ba5-b1899810db2e.png)

2. Modify the **Security Group** of the AMI to allow inbound TCP connections to port **5555**. This is required for remote adb connection to Genymotion Cloud VM.

![Allow ADB Connection](https://user-images.githubusercontent.com/4301109/81505878-9b979480-92c0-11ea-9456-32cf5254d381.png)

3. Access Genymotion Cloud VM by navigating to it's Public IP. The default username is `genymotion` and the password is EC2 instance id. 
[More Info](https://docs.genymotion.com/paas/02_Getting_Started/021_AWS/)

4. Go to Configuration and Enable ADB

![Enable ADB in Genymotion Cloud](https://user-images.githubusercontent.com/4301109/81505975-46a84e00-92c1-11ea-82a5-8912f96849b1.png)

5. From your local machine, ensure that you can connect to Genymotion Cloud VM via adb.

```bash
adb connect <public_ip>:5555
adb devices
```
![ADB connect](https://user-images.githubusercontent.com/4301109/81506018-9be45f80-92c1-11ea-8486-fcac8daee7be.png)

6. Set the environment variable `MOBSF_ANALYZER_IDENTIFIER` as `<public_ip>:5555` when you run the MobSF docker image (Example: `3.81.202.69:5555`).

7. You can now perform MobSF Dynamic Analysis with Genymotion Cloud VM in AWS.

## Corellium Android VM

?> Supports **rooted userdebug** builds, arm64 architecture Android **7.1.2 - 11.0**, upto **API 30**

!> You must not choose non-rooted **user** builds. MobSF requires rooted **userdebug** builds.

1. After creating a supported rooted **userdebug** Android device, Follow Corellium's `Connect via VPN` instructions.

![Corellium Android](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/f384421c-98af-47b1-8d98-29641d9ca974)

2. Do connect to Corellium network using provided VPN configuration.

3. Run `adb connect` locally to ensure that the connection is working from your host.

![Corellium adb](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/c6f1135e-b1ef-4a14-b9bf-6ebfab2e3cca)

4. Set the environment variable `MOBSF_ANALYZER_IDENTIFIER` as `<private_ip>:<port>` of Corellium Android device when you run the MobSF docker image (Example: `10.11.1.1:5001`).


## Corellium iOS VM

Supports jailbroken Corellium iOS VMs from MobSF v3.8.0 onwards.

!> Non jailbroken devices cannot be used with MobSF.

1. After setting up Corellium account, create an API key from https://app.corellium.com/profile/api

![Corellium API](https://user-images.githubusercontent.com/4301109/289017703-b6f25054-d1b5-4c0e-a781-68b18260fb6a.png)

2. Set the API key in the environment variable `MOBSF_CORELLIUM_API_KEY`. If you are using enterprise version of Corellium using a different domain. You must also supply the environment variable `MOBSF_CORELLIUM_API_DOMAIN` with the correct domain value.

3. To enable MobSF HTTPs proxying, You will have to configure the proxy settings in the iOS VM. Go to iPhone `Settings` -> `Wi-Fi` -> Choose the `Corellium` WiFi -> Scroll down and choose `Configure Proxy` -> Choose`Manual configuration` -> Set the `Server` as `127.0.0.1` and `Port` as `1337` -> Click `Save`.

![iOS HTTPS Proxy](https://user-images.githubusercontent.com/4301109/289017713-ffc54f0e-1c23-484d-a612-0318ad41e7a3.png)

4. Run MobSF and now you can create or manage jailbroken iOS VMs with Corellium for Dynamic Analysis.
