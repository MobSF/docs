
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


# 安装


**在 Windows 10, Ubuntu (18.04, 19.04) , macOS Catalina 测试**

!> 请确认首先安装了所有 要求 里的内容


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

?> Windows用户在运行`setup.bat`之前，请关闭所有MobSF打开过的文件夹和用MobSF打开过的文本编辑器。 这些都会因为引起权限错误造成安装中断。


# 运行MobSF

## Linux/Mac

```bash
./run.sh 127.0.0.1:8000
```

***

## Windows

```batch
run.bat 127.0.0.1:8000
```

!> 如果你在执行脚本时没有附带任何参数，那么 MobSF 将监听 `0.0.0.0:8000`。

在你的Web浏览器中，跳转到 `http://localhost:8000/` 以访问 MobSF Web界面。

# 动态分析


## Genymotion Android
?> 支持 x86, x86_x64 体系架构 Android **4.1 - 11.0**, 最高支持 **API 30**

Genymotion是首选的动态分析环境，你可以以最小的损耗来进行设置。 **在启动MobSF之前运行Genymotion Android VM。**所有内容都会在运行时自动配置。我们建议使用**Android 7.0**及更高版本。

* **Android 5.0 - 11.0** -这些版本使用 **Frida**，开箱即用，无需设置。
* **Android 4.1 - 4.4** - 这些版本使用 **Xposed Framework** 并要求您在首次进行Dynamic Analysis之前先移动运行时。这些版本还要求在安装Xposed模块后重新引导VM。

单击动态分析器页面中的 **MobSFy Android Runtime** 按钮以分析 Android运行时环境。

![MobSFy](https://user-images.githubusercontent.com/4301109/77839885-11033780-714f-11ea-9d52-df7b0bd314a0.png)

**HTTPS 代理**

* 对于Android版本 **4.4 - 11.0**, 全局代理设置自动应用于运行时
* 对于Android版本 **4.1 - 4.3**, 设置“动态分析器”页面中显示的Android VM代理。

如果Dynamic Analyzer无法检测到您的android设备，则需要在 `<user_home_dir>/.MobSF/config.py` 中手动配置 `ANALYZER_IDENTIFIER`。

示例: `ANALYZER_IDENTIFIER = '192.168.56.101:5555'`.
你可以从Genymotion标题栏中找到Android设备IP，默认端口为“ 5555”。

![动态分析IP](https://user-images.githubusercontent.com/4301109/65379210-0b312300-dce2-11e9-8827-f63d3b95dfd1.png)

## Android Studio 模拟器
?> 支持arm，arm64和x86架构 Android **5.0 - 9.0**, 最高 **API 28**

带有Google Play商店的Android模拟器映像被视为正式映像，你不能在MobSF中使用它。
在没有Google Play商店的情况下**创建一个Android虚拟设备（AVD）**。不要从Android Studio启动AVD，而应使用“emulator”命令行选项用以可写入的方式启动。

为此，将您的Android SDK仿真器目录添加到`PATH`。

一些示例路径

* Mac - `/Users/<user>/Library/Android/sdk/emulator`
* Linux - `/home/<user>/Android/Sdk/emulator`
* Windows - `C:\Users\<user>\AppData\Local\Android\Sdk\emulator`

**列出可用的Android虚拟设备(AVD)**

```bash
$ emulator -list-avds
Pixel_2_API_29
Pixel_3_API_28
Pixel_XL_API_24
Pixel_XL_API_25
```

!>仅支持**API 28**以下的Android图像！!


设置 `ADB_BINARY` 路径在 `<user_home_dir>/.MobSF/config.py`.

确保您使用的是Android Studio附带的adb二进制文件。如果使用其他版本，则可能会导致冲突并在尝试动态分析时引入问题。

一些示例位置

```python
ADB_BINARY = '/Users/<user>/Library/Android/sdk/platform-tools/adb' # Mac
ADB_BINARY = '/home/<user>/Android/Sdk/platform-tools/adb' # Linux
ADB_BINARY = 'C:\\Users\\<user>\\AppData\\Local\\Android\\Sdk\\platform-tools\\adb.exe' # Windows
ADB_BINARY = 'C:/Users/<user>/AppData/Local/Android/sdk/platform-tools/adb.exe' # Windows
```

**执行Android虚拟设备 (AVD)**

执行一个 AVD **在启动 MobSF 之前** 使用 `emulator` 命令行参数. 

```bash
$ emulator -avd <non_production_avd_name> -writable-system -no-snapshot
```

一切都会在运行时自动配置。 MobSF需要AVD版本**5.0到9.0**进行动态分析。我们建议使用**Android 7.0**及更高版本。

**HTTPS 代理**

* 对于Android版本**5.0-9.0**，全局代理设置会在运行时自动应用。

**GApps 在 AVD (可选)**

如果需要GApp，请从<https://opengapps.org/>查找合适的软件包

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

?> 支持 x86, x86_x64 Android 架构 **5.1 - 11.0**, 最高支持 **API 30**

**在启动MobSF之前**，请在 Cloud 中运行Genymotion Android VM并通过adb连接到它。所有内容都会在运行时自动配置。我们建议使用 **Android 7.0** 及更高版本。

本文档以Amazon Web Services（AWS）为例。您需要在Genymotion Cloud SaaS，Microsoft Azure，Google Cloud Platform或阿里云中执行类似的步骤。

1.使用[Genymotion AMI](https://aws.amazon.com/marketplace/seller-profile?id=933724b4-d35f-4266-905e-e52e4792bc45) 启动EC2实例

![AWS Genymotion AMI](https://user-images.githubusercontent.com/4301109/81505732-7bb3a100-92bf-11ea-9ba5-b1899810db2e.png)

2.修改AMI的 **安全组** 以允许到端口5555的入站TCP连接。到Genymotion Cloud VM的远程adb连接是必需的。

![允许 ADB 连接](https://user-images.githubusercontent.com/4301109/81505878-9b979480-92c0-11ea-9456-32cf5254d381.png)

3.通过导航到公共IP访问Genymotion Cloud VM。默认用户名为 `genymotion`，密码为EC2实例ID。
[更多信息](https://docs.genymotion.com/paas/8.0/02_Getting_Started/021_AWS.html#create-and-set-up-an-instance)

4.转到配置并启用ADB

![在Genymotion Cloud 中启用ADB](https://user-images.githubusercontent.com/4301109/81505975-46a84e00-92c1-11ea-82a5-8912f96849b1.png)

5.从本地计算机，确保可以通过adb连接到Genymotion Cloud VM

```bash
adb connect <public_ip>:5555
adb devices
```

![ADB connect](https://user-images.githubusercontent.com/4301109/81506018-9be45f80-92c1-11ea-8486-fcac8daee7be.png)

6. 现在，您可以使用AWS中的Genymotion Cloud VM执行MobSF动态分析。

如果Dynamic Analyzer没有检测到Cloud VM，则需要在 `<user_home_dir>/.MobSF/config.py` 中手动配置 `ANALYZER_IDENTIFIER`。

例如: `ANALYZER_IDENTIFIER = '<public_ip>:5555'`.

如果MobSF无法检测到adb，则需要在 `<user_home_dir>/.MobSF/config.py` 中配置 `ADB_BINARY` .

例如: `ADB_BINARY = '/Applications/Genymotion.app/Contents/MacOS/tools/adb'`.

# 更新MobSF

如果要更新MobSF，在大多数情况下，您可能必须执行数据库迁移，否则将看到诸如以下的错误：

```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named 
```

运行以下命令以迁移数据库

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

!> 如果上述更改都不起作用，您可能必须删除 `~/.MobSF` 或 `C:\Users\<user>\.MobSF` 并再次运行 setup.sh 或 setup.bat，这将删除之前的扫描结果。

# 运行测试
我们使用tox进行测试。 在 virtualenv 外部安装tox。
```bash
pip install tox
```

**用于风格检查**
```bash
tox -e lint
```


**用于运行风格检查和测试**
```bash
tox -e lint,test
```

