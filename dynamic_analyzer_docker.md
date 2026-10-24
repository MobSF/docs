# Dynamic Analyzer

MobSF supports **certain** rooted/stock Android VMs/emulators, physical Android devices, and jailbroken iOS targets:

* [Genymotion Desktop](https://www.genymotion.com/download/)
* [Genymotion Cloud](https://www.genymotion.com/cloud/)
* [Android Studio Emulator](https://developer.android.com/studio)
* [Corellium Android](https://support.corellium.com/devices/android) 
* [Physical Android device](#physical-android-device) (rooted or stock)
* [Corellium iOS](https://support.corellium.com/devices/ios)
* [Jailbroken iOS device](#jailbroken-ios-device-ssh)

?> From MobSF v4.6.0, an Android VM that cannot be prepared with root, or that is newer than **API 30**, falls back to **Frida Gadget** on Android 5.0 and above. See [Frida Gadget mode](#frida-gadget-mode).

## Genymotion Android
?> Supports arm64, x86, x86_64 architecture Android **4.1 - 11.0**, upto **API 30**

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
?> Supports arm, arm64, x86 and x86_64 architecture Android **5.0 - 11.0**, upto **API 30**

Install or upgrade your Android Studio to the latest. Android Emulator image with Google Play Store is considered as production image and you cannot use that with MobSF as those images **does not have root** access.

Create an Android Virtual Device (AVD) **without Google Play Store**.

!> You must not choose non-rooted **production** images. MobSF requires rooted images without Google Playstore pre-installed.

![Create AVD](https://github.com/user-attachments/assets/5871ff00-2386-4f32-be37-1d749825b069)


After creating the AVD, run it once and make sure everything is alright. Close it along with Android Studio if it's running.

!> Full rooted support is limited to AVDs up to **version 11, API 30**, because newer AVDs do not offer a writable `/system`. From MobSF v4.6.0, newer AVDs and production images use [Frida Gadget mode](#frida-gadget-mode) instead.

**Run Android Virtual Device (AVD)**

Run an AVD **before starting MobSF** using `scripts/start_avd.sh` or `scripts/start_avd.ps1`

```bash
# Run the script to list out available AVDs
scripts/start_avd.sh 
Available AVDs:

Medium_Phone_API_35
Pixel_5_API_30
Pixel_6a_API_29

Use any Android AVD 5.0 - 11.0, up to API 30 without Google Play (production image).
Usage: scripts/start_avd.sh AVD_NAME [START_PORT] [open_gapps.zip path]
Example: scripts/start_avd.sh Pixel_6_Pro_API_28 5554 /path/to/open_gapps.zip

# Choose the AVD you created, make sure it is a non-production AVD.
# MobSF will not work with production AVDs.

scripts/start_avd.sh Pixel_5_API_30
```
Identify the emulator serial number. In this example, the identifier is `emulator-5554`.

![Android AVD](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/e9e849b6-69ad-47a4-8693-c75a0e1aa7cb)


Set the environment variable `MOBSF_ANALYZER_IDENTIFIER` as `emulator-5554` when running MobSF docker image.


**HTTPS Proxy**

* For Android versions **5.0 - 8.0**, MobSF attempts to set global proxy, but might fail due to a bug in adb. Configure proxy settings manually in such cases.
* For Android version **9.0** and above, global proxy settings are automatically applied at runtime.

**GApps on AVD (Optional)**

If you need Google Playstore, download the appropriate package from <https://opengapps.org/>.
Run the `start_avd` script with path to the GApps zip file. This is currently not supported in Windows. You will have to manually do the necessary steps.

```bash
$ scripts/start_avd.sh Pixel_6a_API_29 5554 ~/Downloads/open_gapps-arm64-10.0-stock-20220215.zip
```

## Genymotion Cloud VM
?> Supports arm64, x86, x86_64 architecture Android **5.1 - 11.0**, upto **API 30**

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

## Physical Android device

?> Supported from MobSF **v4.6.0**. Rooted devices and stock (non-rooted) devices running Android **5.0** and above.

1. Enable **Developer options** and **USB debugging** on the device, then confirm that `adb devices` lists it as `device` (not `unauthorized`).
2. Connect over USB, or over Wi-Fi with `adb tcpip 5555` followed by `adb connect <device_ip>:5555`.

MobSF picks a mode for the device:

* **Rooted** - used when `su` grants root without a prompt (for example Magisk with root granted to the Shell app) and `/data/local/tmp` is writable. A writable `/system` is **not** required.
* **Frida Gadget** - used on stock devices that are not rooted, when rooted Frida instrumentation fails, or when you choose it.

### Frida Gadget mode

MobSF injects Frida Gadget into the app, re-signs it, and installs the patched build. This works without root on Android 5.0 and above.

* The app must be scanned first with MobSF Static Analyzer. Apps available only on the device must first be pulled and a static analysis performed.
* Split APK sets (`.apks` and `.xapk`) are supported. MobSF installs the base APK and the splits that match the device.
* Re-signing changes the app signature.

### Physical devices with MobSF in Docker

A container cannot see USB devices. Either connect the device over Wi-Fi (step 2 above), or let the container use the host's ADB server:

1. On the host, run the ADB server so it accepts connections from the container: `adb kill-server && adb -a nodaemon server start`.
2. Restrict port `5037` with a firewall so only the Docker host can reach it. An open ADB server gives full control of every attached device.
3. Run MobSF with `-e ADB_SERVER_SOCKET=tcp:host.docker.internal:5037` (on Linux, also add `--add-host=host.docker.internal:host-gateway`).


## Corellium iOS VM

Corellium iOS VM must have Frida Server >17.0.0 installed from MobSF v4.4.0 onwards.

!> Non jailbroken devices cannot be used with MobSF.

1. After setting up Corellium account, create an API key from https://app.corellium.com/profile/api

![Corellium API](https://user-images.githubusercontent.com/4301109/289017703-b6f25054-d1b5-4c0e-a781-68b18260fb6a.png)

2. Set the API key in the environment variable `MOBSF_CORELLIUM_API_KEY`. If you are using enterprise version of Corellium using a different domain. You must also supply the environment variable `MOBSF_CORELLIUM_API_DOMAIN` with the correct domain value.

3. To enable MobSF HTTPs proxying, You will have to configure the proxy settings in the iOS VM. Go to iPhone `Settings` -> `Wi-Fi` -> Choose the `Corellium` WiFi -> Scroll down and choose `Configure Proxy` -> Choose`Manual configuration` -> Set the `Server` as `127.0.0.1` and `Port` as `1337` -> Click `Save`.

![iOS HTTPS Proxy](https://user-images.githubusercontent.com/4301109/289017713-ffc54f0e-1c23-484d-a612-0318ad41e7a3.png)

4. Run MobSF and now you can create or manage jailbroken iOS VMs with Corellium for Dynamic Analysis.

## Jailbroken iOS device (Beta)

!> This feature is in **early beta**. It has so far been tested on **iPhone 6s** and **iPhone 8** with **checkra1n** and **palera1n** jailbreak. Please reach out in our **Slack** channel if something looks broken.

MobSF supports a **physical jailbroken iOS device** from v4.5.1 onwards. Connectivity can be over **Wi‑Fi** (device IP) or **USB** (e.g. port forwarding so MobSF reaches `127.0.0.1` or `host.docker.internal` from the container).

0. On the host that attaches the iPhone over **USB**, install **libimobiledevice** so `iproxy` and the `idevice*` tools are available (USB port forwarding and device checks). **macOS:** `brew install libimobiledevice`. **Debian/Ubuntu:** `sudo apt install libimobiledevice-utils`.
1. Ensure OpenSSH (or your jailbreak’s SSH) is reachable and credentials match what you configure below.
2. Set **`MOBSF_IOS_ANALYZER_IDENTIFIERS`** to the SSH socket(s): `IP:PORT`. Examples: `192.168.1.100:22`, or multiple devices: `192.168.1.100:22,192.168.1.101:22`.
3. Optionally set **`MOBSF_IOS_SSH_USER`** and **`MOBSF_IOS_SSH_PASSWORD`** if they differ from the defaults (`root` / `alpine`).
4. Ideally connect MobSF host and the iPhone to same WiFi/LAN network. To enable MobSF HTTPs proxying, You will have to configure the proxy settings in the iOS device. Go to iPhone `Settings` -> `Wi-Fi` -> Choose the WiFi SSID -> Scroll down and choose `Configure Proxy` -> Choose`Manual configuration` -> Set the `Server` as `<ip address of mobsf host>` and `Port` as `1337` -> Click `Save`.
