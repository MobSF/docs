# Requirements
Requirements for setting up MobSF locally.

System Requirements: 8GB+ RAM, 3GHz CPU, 50GB+ Free Space

Operating Systems: Mac, Linux, Windows

## Static Analysis
* **Mac**
  * Install [Git](https://www.atlassian.com/git/tutorials/install-git)
  * Install [Python **3.10+**](https://www.python.org/)
  * After installing Python 3.10+, go to `/Applications/Python 3.10/` and run `Update Shell Profile.command` first and then `Install Certificates.command`
  * Install [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)
  * Install command line tools `xcode-select --install`
  * Download & Install [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) as per the [wiki instructions](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)
  * Windows App Static analysis requires a Windows Host or Windows VM for Mac and Linux. [More Info](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md)


* **Ubuntu/Debian based Linux**:
  * Install Git `sudo apt-get install git`
  * Install Python **3.10+** `sudo apt-get install python3.10`
  * Install JDK 8+ `sudo apt-get install openjdk-8-jdk`
  * Install the following dependencies
    ```bash
    sudo apt install python3-dev python3-venv python3-pip build-essential libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev wkhtmltopdf
    ```
  * Windows App Static analysis requires a Windows Host or Windows VM for Mac and Linux. [More Info](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md)

* **Windows**
  * Install [Git](https://git-scm.com/download/win)
  * Install [Python **3.10+**](https://www.python.org/)
  * Install [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)
  * Install [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)
  * Install [OpenSSL (non-light)](https://slproweb.com/products/Win32OpenSSL.html)
  * Download & Install [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) as per the [wiki instructions](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)
  * Add the folder that contains `wkhtmltopdf` binary to environment variable PATH.


?> **IMPORTANT:** Set `JAVA_HOME` environment variable. iOS IPA Analysis works only on **Mac, Linux and Docker containers**.

***

# Installation

**Tested on Windows 10, Ubuntu (18.04, 19.04) , macOS Catalina**

!> Please make sure that all the requirements mentioned are installed first.

```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
```

## Linux/Mac
```bash
./setup.sh
```

## Windows
```batch
setup.bat
```

?> Windows users, before running `setup.bat` close any opened folders of MobSF or text editors with MobSF opened. Either of these can interrupt the setup by causing permission errors.

***

# Running MobSF

## Linux/Mac
```bash
./run.sh 127.0.0.1:8000
```

## Windows

```batch
run.bat 127.0.0.1:8000
``` 

!> MobSF server will listen on `0.0.0.0:8000` if you use the run script without arguments.

In your web browser, navigate to `http://localhost:8000/` to access MobSF web interface.

***

# Dynamic Analysis

You need one of the following Android/iOS virtual device for Dynamic Analysis.

* [Genymotion Desktop](https://www.genymotion.com/download/)
* [Genymotion Cloud](https://www.genymotion.com/cloud/)
* [Android Studio Emulator](https://developer.android.com/studio)
* [Corellium Android](https://support.corellium.com/getting-started/introduction-to-virtual-devices/quickstart-for-android) 
* [Corellium iOS](https://support.corellium.com/getting-started/introduction-to-virtual-devices/quickstart-for-ios)

!> Dynamic analysis using real mobile device is possible for Android, **but not supported by us.** 

## Genymotion Android
?> Supports x86, x86_64 architecture Android **4.1 - 11.0**, upto **API 30**

Genymotion is the preferred dynamic analysis environment that you can setup with the least friction. Run a Genymotion Android VM **before starting MobSF.** Everything will be configured automatically at runtime. We recommend using **Android 7.0** and above.

* **Android 5.0 - 11.0** - These versions uses **Frida** and works out of the box with zero configuration or setup.
* **Android 4.1 - 4.4** - These versions uses **Xposed Framework** and requires that you should MobSFy the runtime prior to Dynamic Analysis for the first time. These versions also require VM reboot after installing Xposed Modules.

Click **MobSFy Android Runtime** button in Android Dynamic Analyzer page to MobSFy the android runtime environment.

![MobSFy](https://user-images.githubusercontent.com/4301109/77839885-11033780-714f-11ea-9d52-df7b0bd314a0.png)

**HTTPS Proxy**

* For Android versions **4.4 - 11.0**, global proxy settings are automatically applied at runtime.
* For Android version **4.1 - 4.3**, set Android VM proxy as displayed in Dynamic Analyzer page.

If MobSF Dynamic Analyzer doesn't detect your android device, set the device identifier via the environment variable `MOBSF_ANALYZER_IDENTIFIER` before running MobSF.

Example: `MOBSF_ANALYZER_IDENTIFIER = '192.168.56.101:5555'`.
You can find the Android Device IP from the Genymotion title bar and the default port is `5555`.

![Dynamic Analyzer IP](https://user-images.githubusercontent.com/4301109/65379210-0b312300-dce2-11e9-8827-f63d3b95dfd1.png)

## Android Studio Emulator
?> Supports arm, arm64, x86 and x86_64 architecture Android **5.0 - 9.0**, upto **API 28**

Android Emulator image with Google Play Store is considered as production image and you cannot use that with MobSF.
Create an Android Virtual Device (AVD) **without Google Play Store**. Do not start the AVD from Android Studio, instead start the AVD with writable system using `emulator` command line options. 

For that, add your Android SDK emulator directory to `PATH`.

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

!>Only Android images upto **API 28** are supported!


Set `ADB_BINARY` path in `<user_home_dir>/.MobSF/config.py`.

Make sure that you are using the adb binary that comes with Android Studio. If you use a different version, that might cause conflicts and introduce issues while attempting dynamic analysis.

Some example locations

```python
ADB_BINARY = '/Users/<user>/Library/Android/sdk/platform-tools/adb' # Mac
ADB_BINARY = '/home/<user>/Android/Sdk/platform-tools/adb' # Linux
ADB_BINARY = 'C:\\Users\\<user>\\AppData\\Local\\Android\\Sdk\\platform-tools\\adb.exe' # Windows
ADB_BINARY = 'C:/Users/<user>/AppData/Local/Android/sdk/platform-tools/adb.exe' # Windows
```

**Run Android Virtual Device (AVD)**

Run an AVD **before starting MobSF** using `emulator` command line options. 

```bash
$ emulator -avd <non_production_avd_name> -writable-system -no-snapshot
```

Everything will be configured automatically at runtime. MobSF requires AVD version **5.0 to 9.0** for dynamic analysis. We recommend using **Android 9.0, API 28** as older versions have known bugs and breaks certain features like adb reverse tcp which is required for MobSF HTTPs proxy to work.

**HTTPS Proxy**

* For Android versions **5.0 - 8.0**, MobSF attempts to set global proxy, but might fail due to a bug in adb. Configure proxy settings manually in such cases.
* For Android version **9.0**, global proxy settings are automatically applied at runtime.

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

## Genymotion Cloud Android
?> Supports x86, x86_64 architecture Android **5.1 - 11.0**, upto **API 30**

Run a Genymotion Android VM in cloud and connect to it via adb **before starting MobSF.** Everything will be configured automatically at runtime. We recommend using **Android 7.0** and above.

This documentation uses Amazon Web Services (AWS) as an example. You need to follow similar steps in Genymotion Cloud SaaS, Microsoft Azure, Google Cloud Platform, or Alibaba Cloud.

1. Launch an EC2 instance with [Genymotion AMI](https://aws.amazon.com/marketplace/seller-profile?id=933724b4-d35f-4266-905e-e52e4792bc45)

![AWS Genymotion AMI](https://user-images.githubusercontent.com/4301109/81505732-7bb3a100-92bf-11ea-9ba5-b1899810db2e.png)

2. Modify the **Security Group** of the AMI to allow inbound TCP connections to port **5555**. This is required for remote adb connection to Genymotion Cloud VM.

![Allow ADB Connection](https://user-images.githubusercontent.com/4301109/81505878-9b979480-92c0-11ea-9456-32cf5254d381.png)

3. Access Genymotion Cloud VM by navigating to it's Public IP. The default username is `genymotion` and the password is EC2 instance id. 
[More Info](https://docs.genymotion.com/paas/8.0/02_Getting_Started/021_AWS.html#create-and-set-up-an-instance)

4. Go to Configuration and Enable ADB

![Enable ADB in Genymotion Cloud](https://user-images.githubusercontent.com/4301109/81505975-46a84e00-92c1-11ea-82a5-8912f96849b1.png)

5. From your local machine, ensure that you can connect to Genymotion Cloud VM via adb.

```bash
adb connect <public_ip>:5555
adb devices
```
![ADB connect](https://user-images.githubusercontent.com/4301109/81506018-9be45f80-92c1-11ea-8486-fcac8daee7be.png)

6. You can now perform MobSF Dynamic Analysis with Genymotion Cloud VM in AWS.

If MobSF Dynamic Analyzer doesn't detect your Cloud VM, set the device identifier via the environment variable `MOBSF_ANALYZER_IDENTIFIER` before running MobSF.

Example: `MOBSF_ANALYZER_IDENTIFIER = '<public_ip>:5555'`.

If MobSF cannot detect adb, you need to configure `ADB_BINARY` in `<user_home_dir>/.MobSF/config.py`.

Example: `ADB_BINARY = '/Applications/Genymotion.app/Contents/MacOS/tools/adb'`.

## Corellium Android VM

?> Supports **rooted userdebug** builds, arm64 architecture Android **7.1.2 - 11.0**, upto **API 30**

!> You must not choose non-rooted **user** builds. MobSF requires rooted **userdebug** builds.

1. After creating a supported rooted **userdebug** Android device, Follow Corellium's `Connect via VPN` instructions.

![Corellium Android](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/f384421c-98af-47b1-8d98-29641d9ca974)

2. Do connect to Corellium network using provided VPN configuration.

3. Run `adb connect` locally to ensure that the connection is working from your host.

![Corellium adb](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/c6f1135e-b1ef-4a14-b9bf-6ebfab2e3cca)

4. Set the environment variable `MOBSF_ANALYZER_IDENTIFIER` as `<private_ip>:<port>` of Corellium Android device before running MobSF. (Example: `10.11.1.1:5001`).


## Corellium iOS VM

Supports jailbroken Corellium iOS VMs from MobSF v3.8.0 onwards.

!> Non jailbroken devices cannot be used with MobSF. Real devices are not supported at this time.

1. After setting up Corellium account, create an API key from https://app.corellium.com/profile/api

![Corellium API](https://user-images.githubusercontent.com/4301109/289017703-b6f25054-d1b5-4c0e-a781-68b18260fb6a.png)

2. Set the API key in the environment variable `MOBSF_CORELLIUM_API_KEY`

3. To enable MobSF HTTPs proxying, You will have to configure the proxy settings in the iOS VM. Go to iPhone `Settings` -> `Wi-Fi` -> Choose the `Corellium` WiFi -> Scroll down and choose `Configure Proxy` -> Choose`Manual configuration` -> Set the `Server` as `127.0.0.1` and `Port` as `1337` -> Click `Save`.

![iOS HTTPS Proxy](https://user-images.githubusercontent.com/4301109/289017713-ffc54f0e-1c23-484d-a612-0318ad41e7a3.png)

4. Run MobSF and now you can create or manage jailbroken iOS VMs with Corellium for Dynamic Analysis.

***

# Updating MobSF

## Linux/Mac/Windows

```bash
cd Mobile-Security-Framework-MobSF/
git pull origin master
poetry update
poetry run python3 manage.py makemigration
poetry run python3 manage.py makemigrations StaticAnalyzer
poetry run python3 manage.py migrate
```

!> If database migration fails, you will have to delete (Linux or Mac: `~/.MobSF`, Windows: `C:\Users\<user>\.MobSF`) directory and run (Linux/Mac: `setup.sh`, Windows: `setup.bat`) again. This will delete previous scan results and data.

***

# Running Tests

We use tox for running tests.
```bash
pip install tox
```

**For linting**
```bash
tox -e lint
```

**For running lint + test**
```bash
tox -e lint,test
```
