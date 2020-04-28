# 动态分析

!> 可以使用真实的移动设备进行动态分析，**但我们不支持。**如果您需要动态分析，请不要在Docker或虚拟机中设置MobSF。

## Genymotion Android x86
?> 支持X86体系架构 Android **4.1 - 9.0**, 最高支持 **API 28**

Genymotion是首选的动态分析环境，你可以以最小的损耗来进行设置。 **在启动MobSF之前运行Genymotion Android VM。**所有内容都会在运行时自动配置。我们建议使用**Android 7.0**及更高版本。

* **Android 5.0-9.0** -这些版本使用 **Frida**，开箱即用，无需设置。
* **Android 4.1 - 4.4** - 这些版本使用 **Xposed Framework** 并要求您在首次进行Dynamic Analysis之前先移动运行时。这些版本还要求在安装Xposed模块后重新引导VM。

单击动态分析器页面中的 **MobSFy Android Runtime** 按钮以分析 Android运行时环境。

![MobSFy](https://user-images.githubusercontent.com/4301109/77839885-11033780-714f-11ea-9d52-df7b0bd314a0.png)

**HTTPS 代理**

* 对于Android版本 **4.4 - 9.0**, 全局代理设置自动应用于运行时
* 对于Android版本 **4.1 - 4.3**, 设置“动态分析器”页面中显示的Android VM代理。

如果Dynamic Analyzer无法检测到您的android设备，则需要在 `MobSF/settings.py` 中手动配置 `ANALYZER_IDENTIFIER`。

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


设置 `ADB_BINARY` 路径在 `MobSF/settings.py`.

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
