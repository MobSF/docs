
# Requirements
## Static Analysis
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
  * Install [Anaconda Python **3.7** (3.8 is not supported)](https://repo.anaconda.com/archive/Anaconda3-2020.02-Windows-x86_64.exe)
  * Install [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)
  * Install [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)
  * Install [OpenSSL](https://slproweb.com/download/Win64OpenSSL-1_1_1d.exe)
  * Download & Install [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) as per the [wiki instructions](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)
  * Add the folder that contains `wkhtmltopdf` binary to environment variable PATH.


?> **IMPORTANT:** Set `JAVA_HOME` environment variable. iOS IPA Analysis works only on **Mac, Linux and Docker containers**.

***
## Dynamic Analysis
* **Dynamic Analysis will not work if you use MobSF docker container or setup MobSF inside a Virtual Machine.**
* Install [Genymotion](https://www.genymotion.com/fun-zone/) or [Android Studio Emulator](https://developer.android.com/studio)

