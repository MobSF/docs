
# 要求

## 静态分析

* **Mac**
  * 安装 [Git](https://www.atlassian.com/git/tutorials/install-git)
  * 安装 [Python **3.8-3.9**](https://www.python.org)
  * After installing Python 3.8+, go to  `/Applications/Python 3.8/` and run `Update Shell Profile.command` and `Install Certificates.command`
  * 安装 [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)
  * 安装命令行工具 `xcode-select --install`
  * 下载和安装 [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) 按照 [WIKI操作指南](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)
  * macOS Mojave 用户, 请安装 headers（如果可用）：

    ```bash
    sudo installer -pkg /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg -target /
    ```

  * Windows App静态分析需要Mac和Linux的Windows主机或Windows VM。 [更多信息](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md)


* **操作指南**:
  * 安装 Git `sudo apt-get install git`
  * 安装 Python **3.8-3.9** `sudo apt-get install python3.8`
  * 安装 JDK 8+ `sudo apt-get install openjdk-8-jdk`
  * 安装以下依赖项

    ```bash
    sudo apt install python3-dev python3-venv python3-pip build-essential libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev wkhtmltopdf
    ```

  * Windows App静态分析需要Mac和Linux的Windows主机或Windows VM。 [更多信息](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md)

* **Windows**
  * 安装 [Git](https://git-scm.com/download/win)
  * 安装 [Python **3.8-3.9**](https://www.python.org/)
  * 安装 [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)
  * 安装 [Microsoft Visual C++ Build Tools](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)
  * 安装 [OpenSSL (non-light)](https://slproweb.com/products/Win32OpenSSL.html)
  * 下载和安装 [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) as per the [WIKI操作指南](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)
  * 将包含 `wkhtmltopdf` 二进制文件的文件夹添加到环境变量PATH。


?> **重要提示：**设置`JAVA_HOME`环境变量。 iOS IPA Analysis仅适用于**Mac，Linux和Docker容器**。

***

## 动态分析

* **如果您使用MobSF docker容器或在虚拟机中设置MobSF，则动态分析将不起作用。**
* 安装 [Genymotion](https://www.genymotion.com/fun-zone/) 或者 [Android Studio Emulator](https://developer.android.com/studio)

