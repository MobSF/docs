# Requirements
Requirements for setting up MobSF locally.

## Static Analysis
* **Mac**
  * Install [Git](https://www.atlassian.com/git/tutorials/install-git)
  * Install [Python **3.8-3.9**](https://www.python.org/)
  * After installing Python 3.8+, go to `/Applications/Python 3.8/` and run `Update Shell Profile.command` first and then `Install Certificates.command`
  * Install [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)
  * Install command line tools `xcode-select --install`
  * Download & Install [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) as per the [wiki instructions](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)
  * Windows App Static analysis requires a Windows Host or Windows VM for Mac and Linux. [More Info](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md)


* **Ubuntu/Debian based Linux**:
  * Install Git `sudo apt-get install git`
  * Install Python **3.8-3.9** `sudo apt-get install python3.8`
  * Install JDK 8+ `sudo apt-get install openjdk-8-jdk`
  * Install the following dependencies
    ```bash
    sudo apt install python3-dev python3-venv python3-pip build-essential libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev wkhtmltopdf
    ```
  * Windows App Static analysis requires a Windows Host or Windows VM for Mac and Linux. [More Info](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md)

* **Windows**
  * Install [Git](https://git-scm.com/download/win)
  * Install [Python **3.8-3.9**](https://www.python.org/)
  * Install [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)
  * Install [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)
  * Install [OpenSSL (non-light)](https://slproweb.com/products/Win32OpenSSL.html)
  * Download & Install [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) as per the [wiki instructions](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)
  * Add the folder that contains `wkhtmltopdf` binary to environment variable PATH.


?> **IMPORTANT:** Set `JAVA_HOME` environment variable. iOS IPA Analysis works only on **Mac, Linux and Docker containers**.

***
## Dynamic Analysis
* **Dynamic Analysis will not work if you use MobSF docker container or setup MobSF inside a Virtual Machine.**
* Install [Genymotion](https://www.genymotion.com/fun-zone/) or [Genymotion Cloud VM](https://www.genymotion.com/cloud/) or [Android Studio Emulator](https://developer.android.com/studio)



# Installation

**Tested on Windows 10, Ubuntu (18.04, 19.04) , macOS Catalina**

!> Please make sure that all the requirements mentioned are installed first.


## Linux/Mac
```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
./setup.sh
```
***

## Windows
```batch
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
setup.bat
```

?> Windows users, before running `setup.bat` close any opened folders of MobSF or text editors with MobSF opened. Either of these can interrupt the setup by causing permission errors.


# Running MobSF

## Linux/Mac
```bash
./run.sh 127.0.0.1:8000
```

***

## Windows

```batch
run.bat 127.0.0.1:8000
``` 

!> MobSF will listen to `0.0.0.0:8000` if you use the run script without arguments.

In your web browser, navigate to `http://localhost:8000/` to access MobSF web interface.

# Dynamic Analyzer

!> Dynamic analysis using real mobile device is possible, **but not supported by us.** 

## Genymotion Android
?> Supports x86, x86_64 architecture Android **4.1 - 11.0**, upto **API 30**

Genymotion is the preferred dynamic analysis environment that you can setup with the least friction. Run a Genymotion Android VM **before starting MobSF.** Everything will be configured automatically at runtime. We recommend using **Android 7.0** and above.

* **Android 5.0 - 11.0** - These versions uses **Frida** and works out of the box with zero configuration or setup.
* **Android 4.1 - 4.4** - These versions uses **Xposed Framework** and requires that you should MobSFy the runtime prior to Dynamic Analysis for the first time. These versions also require VM reboot after installing Xposed Modules.

Click **MobSFy Android Runtime** button in Dynamic Analyzer page to MobSFy the android runtime environment.

![MobSFy](https://user-images.githubusercontent.com/4301109/77839885-11033780-714f-11ea-9d52-df7b0bd314a0.png)

**HTTPS Proxy**

* For Android versions **4.4 - 11.0**, global proxy settings are automatically applied at runtime.
* For Android version **4.1 - 4.3**, set Android VM proxy as displayed in Dynamic Analyzer page.

If Dynamic Analyzer doesn't detect your android device, you need to manually configure `ANALYZER_IDENTIFIER` in `<user_home_dir>/.MobSF/config.py` or via environment variable `ANALYZER_IDENTIFIER`.

Example: `ANALYZER_IDENTIFIER = '192.168.56.101:5555'`.
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

Everything will be configured automatically at runtime. MobSF requires AVD version **5.0 to 9.0** for dynamic analysis. We recommend using **Android 7.0** and above.

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

If Dynamic Analyzer doesn't detect the Cloud VM, you need to manually configure `ANALYZER_IDENTIFIER` in `<user_home_dir>/.MobSF/config.py` or via environment variable `ANALYZER_IDENTIFIER`.

Example: `ANALYZER_IDENTIFIER = '<public_ip>:5555'`.

If MobSF cannot detect adb, you need to configure `ADB_BINARY` in `<user_home_dir>/.MobSF/config.py`.

Example: `ADB_BINARY = '/Applications/Genymotion.app/Contents/MacOS/tools/adb'`.


# Updating MobSF

If you are updating MobSF, In most cases you might have to perform database migrations or you will see errors such as
```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named 
```

## Linux/Mac

```bash
cd Mobile-Security-Framework-MobSF/
git pull origin master
. venv/bin/activate
pip install --no-cache-dir --use-deprecated=legacy-resolver -r requirements.txt
python manage.py makemigrations
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
deactivate
```

!> If database migration fails, you will have to delete `~/.MobSF` directory and run `setup.sh` again. This will delete previous scan results and data.

## Windows

```batch
cd Mobile-Security-Framework-MobSF/
git pull origin master
.\venv\Scripts\activate
pip install --no-cache-dir --use-deprecated=legacy-resolver -r requirements.txt
python manage.py makemigrations
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
deactivate
```
!> If database migration fails, you will have to delete `C:\Users\<user>\.MobSF` directory and run `setup.bat` again. This will delete previous scan results and data.


## Running Tests
We use tox for running tests. Install tox outside virtualenv.
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
