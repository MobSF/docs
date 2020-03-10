# MobSF Documentation

***

## Requirements

#### Static Analysis
* **Mac**
  * Install [Git](https://www.atlassian.com/git/tutorials/install-git)
  * Install [Python **3.6 - 3.7** (3.8 is not supported)](https://www.python.org/ftp/python/3.7.5/python-3.7.5-macosx10.6.pkg)
  * macOS Catalina users must uninstall existing python3 and install the one from [Python.org](https://www.python.org/ftp/python/3.7.5/python-3.7.5-macosx10.6.pkg). After installation, go to `/Applications/Python 3.7/` and run `Install Certificates.command` and `Update Shell Profile.command`
  * Install [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)
  * Install command line tools `xcode-select --install`
  * Download & Install [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) as per the [wiki instructions](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)
  * macOS Mojave users, install headers if available:
    ```bash
    sudo installer -pkg /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg -target /
    ```
  * Windows App Static analysis requires a Windows Host or Windows VM for Mac and Linux. [More Info](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/install/windows/readme.md)

* **Ubuntu/Debian based Linux**:
  * Install Git `sudo apt get install git`
  * Install Python **3.6 - 3.7** `sudo apt-get install python3`
  * Install JDK 8+ `sudo apt-get install openjdk-8-jdk`
  * Install the following dependencies
    ```bash
    sudo apt install python3-venv python3-pip python3-dev build-essential libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev wkhtmltopdf
    ```
  * Windows App Static analysis requires a Windows Host or Windows VM for Mac and Linux. [More Info](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/install/windows/readme.md)

* **Windows**
  * Install [Git](https://git-scm.com/download/win)
  * Install [Python **3.7**](https://www.anaconda.com/distribution/#download-section)
  * Install [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)
  * Install [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)
  * Install [OpenSSL](https://slproweb.com/download/Win64OpenSSL-1_1_1d.exe)
  * Download & Install [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) as per the [wiki instructions](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)
  * Add the folder that contains `wkhtmltopdf` binary to environment variable PATH.



**IMPORTANT:**
* Set `JAVA_HOME` environment variable.
* iOS IPA Analysis works only on **Mac, Linux and Docker containers**.

#### Dynamic Analysis
* **Dynamic Analysis will not work if you use MobSF docker container or setup MobSF inside a Virtual Machine.**
* Install [Genymotion](https://www.genymotion.com/fun-zone/)

## Installation

**Tested on Windows 10, Ubuntu (18.04, 19.04) , macOS Catalina**

```
# Please make sure that all the requirements mentioned above are installed first.

git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
# Linux or Mac users
./setup.sh 
# Windows users
setup.bat
```
**IMPORTANT:** Windows users, before running `setup.bat` close any opened folders of MobSF or text editors with MobSF opened. Either of these can interrupt the setup by causing permission errors.

### Running MobSF

* For Linux and Mac: `./run.sh` 
* For Windows: `run.bat` 

You can navigate to `http://localhost:8000/` to access MobSF web interface.

### Configuring Dynamic Analyzer

**Dynamic analysis using a real mobile phone is not supported.**

**Run a Genymotion Android VM before starting MobSF.** Everything will be configured automatically at runtime. MobSF requires Genymotion Android x86 VMs version 4.1 to 9.0 for dynamic analysis. We recommend using Android 7.0 and above.

Android versions 5 and above are automatically MobSFyed on first run. For Android versions less than 5, you must MobSFy the Android Runtime prior to Dynamic Analysis for the first time. Click **MobSFy Android Runtime** button in Dynamic Analysis page to MobSFy the android runtime environment.

**HTTPS Proxy**

* For Android versions 4.4 - 9.0, global proxy settings are automatically applied at runtime.
* For Android version 4.1 - 4.3, set Android VM proxy as displayed in Dynamic Analysis page.

If Dynamic Analyzer doesn't detect your android device, you need to manually configure `ANALYZER_IDENTIFIER` in _MobSF/settings.py_. Example: `ANALYZER_IDENTIFIER = '192.168.56.101:5555'`.
You can find the Android Device IP from the Genymotion title bar and the default port is 5555.

![Dynamic Analyzer IP](https://user-images.githubusercontent.com/4301109/65379210-0b312300-dce2-11e9-8827-f63d3b95dfd1.png)

### MobSF Docker Container

> Lazy to setup MobSF?
Use the latest MobSF docker image. Dynamic Analysis is not supported
```
docker pull opensecurity/mobile-security-framework-mobsf
# Static Analysis Only
docker run -it -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

***
### MobSF e-Learning Courses & Certification

We have 2 self paced e-learning courses that covers MobSF and other Android Security tools
* [OpSecX - Automated Mobile Application Security Assessment with MobSF – MAS (Currently being updated)](https://opsecx.com/index.php/product/automated-mobile-application-security-assessment-with-mobsf/)
* [OpSecX - Android Security Tools Expert – ATX](https://opsecx.com/index.php/product/android-security-tools-expert-atx/)

### Updating MobSF

If you are updating MobSF, In most cases you might have to perform database migrations or you will see errors such as
```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named 
```

Run the below command to migrate your db
```
python manage.py makemigrations
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
```

If the above changes didn't work, you might have to run  `setup.sh` or `setup.bat` again which will delete your previous scan results.

### APKiD

APKiD is enabled by default. 
To disable it, set `APKID_ENABLED` to `False` in `MobSF/settings.py`.

### VirusTotal Scan

VirusTotal Scan is disabled by default. You need to add your VirusTotal API Key before enabling it.

* Get VirusTotal API Key [here](https://www.virustotal.com/#/join-us)
* Access your API Key from https://www.virustotal.com/en/user/[username]/apikey/.
* In `MobSF/settings.py`, add your API Key to `VT_API_KEY` and set `VT_ENABLED` to `True` and restart MobSF.

### AppMonsta Android Play Store Information

We use AppMonsta API to fetch details from Google Play Store as a fail safe to our primary implementation. It is disabled by default. To enable it, you need AppMonsta API Key.

* Get AppMonsta API Key from: [AppMonsta API Key](https://appmonsta.com/dashboard/get_api_key/)
* In `MobSF/settings.py`, add your API Key to `APPMONSTA_KEY` and restart MobSF.


### Mass Static Analysis

MobSF supports mass static analysis: 
[Run Mass Static Analysis with MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF/wiki/4.-Mass-Static-Analysis)

### Using Postgres DB instead of SQLite:

[How to Configure Postgres DB](https://github.com/MobSF/Mobile-Security-Framework-MobSF/wiki/8.-Use-Postgres-Database-Instead-of-Sqlite3)

### Home Directory Support

If you want all user uploads, downloads and user configurations to be created in home directory, enable home directory support: [Home Directory Support](https://github.com/MobSF/Mobile-Security-Framework-MobSF/wiki/5.-Home-Directory-Support)

### Docker Image for MobSF Static Analysis

[MobSF Docker Image and Options](https://github.com/MobSF/Mobile-Security-Framework-MobSF/wiki/7.-Docker-Container-for-MobSF-Static-Analysis)

### REST API

MobSF provides REST APIs. You can access API docs from within the app.

### CI/CD

[MobSF CI/CD Pipeline](https://github.com/MobSF/Mobile-Security-Framework-MobSF/wiki/10.-MobSF-CI-CD)

### Running Tests

You can run all the unit tests with `tox -e lint,test` (lint doesn't work on windows)
