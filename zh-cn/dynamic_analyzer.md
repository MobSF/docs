# 动态分析器

MobSF 支持使用以下命令创建的**某些** root Android VM/模拟器：
* [Genymotion](https://www.genymotion.com/download/)
* [Genymotion 云虚拟机](https://www.genymotion.com/pricing/)
* [Android Studio模拟器](https://developer.android.com/studio)
* [Corellium](https://support.corellium.com/getting-started/introduction-to-virtual-devices/quickstart-for-android)

* MobSF 还支持使用 Corellium 创建的越狱 iOS 虚拟设备

## Genymotion Android
?> 支持 x86、x86_64 架构 Android **4.1 - 11.0**，最高 **API 30**

Genymotion 是您可以轻松设置的首选动态分析环境。 **在启动 MobSF 之前运行 Genymotion Android VM。**我们建议使用 **Android 7.0** 及更高版本。

* **Android 5.0 - 11.0** - 这些版本使用 **Frida** 并且开箱即用，零配置或设置。
* **Android 4.1 - 4.4** - 这些版本使用 **Xposed Framework** 并要求您首次在动态分析之前对运行时进行 MobSFy。这些版本还需要在安装 Xposed 模块后重新启动 VM。

运行Android VM后，您可以从标题栏中看到设备标识符。

![分析器标识符](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/6204cdf4-1bc6-4b9a-a9f6-99db64c2f8e2)

运行 MobSF docker 映像时，将环境变量“MOBSF_ANALYZER_IDENTIFIER”设置为虚拟机的设备标识符（示例：“192.168.58.102:5555”）。

**HTTPS 代理**

* 对于 Android 版本 **4.4 - 11.0**，全局代理设置会在运行时自动应用。
* 对于 Android 版本 **4.1 - 4.3**，请按照动态分析器页面中显示的方式设置 Android VM 代理。


## Android Studio 模拟器
?> 支持arm、arm64、x86和x86_64架构Android **5.0 - 9.0**，最高**API 28**

带有 Google Play 商店的 Android 模拟器映像被视为生产映像，您不能将其与 MobSF 一起使用，因为这些映像没有 root 访问权限。

创建 Android 虚拟设备 (AVD) **无需 Google Play 商店**。

![Create AVD](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/28199a89-847a-411f-9f85-e1179b5f835a)

!> 不要从 Android Studio IDE/AVD Manager UI 启动 AVD，而是按照下面的具体说明进行操作。

**使用模拟器从命令行运行 AVD**

将 Android SDK 模拟器目录附加到“PATH”环境变量中。

一些示例位置

* Mac - `/Users/<user>/Library/Android/sdk/emulator`
* Linux - `/home/<user>/Android/Sdk/emulator`
* Windows - `C:\Users\<user>\AppData\Local\Android\Sdk\emulator`

**列出可用的 Android 虚拟设备 (AVD)**

```bash
$ emulator -list-avds
Pixel_2_API_29
Pixel_3_API_28
Pixel_XL_API_24
Pixel_XL_API_25
```

!> 仅支持 **API 28** 以下的 Android 图像！较新的 Android AVD 不提供可写的“/system”，因此无法与 MobSF 一起使用。


**运行 Android 虚拟设备 (AVD)**

**在启动 MobSF** 之前使用“模拟器”命令行选项运行 AVD。

````bash
$ 模拟器 -avd <非生产 avd_name> -可写系统 -无快照
````

![Android AVD](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/e9e849b6-69ad-47a4-8693-c75a0e1aa7cb)

识别模拟器序列号。在此示例中，标识符是“emulator-5554”。

运行 MobSF docker 镜像时，将“MOBSF_ANALYZER_IDENTIFIER”设置为“emulator-5554”。

MobSF 需要 AVD 版本 **5.0 至 9.0** 进行动态分析。我们建议使用 **Android 7.0** 及更高版本。

**HTTPS 代理**

* 对于 Android 版本 **5.0 - 9.0**，全局代理设置会在运行时自动应用。

**AVD 上的 GApp（可选）**

如果您需要 GApp，请从 <https://opengapps.org/> 找到合适的包

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

## Genymotion 云虚拟机
?> 支持 x86、x86_64 架构 Android **5.1 - 11.0**，最高 **API 30**

**在运行 MobSF 之前，在云中运行 Genymotion Android VM。**我们建议使用 **Android 7.0** 及更高版本。

本文档使用 Amazon Web Services (AWS) 作为示例。您需要在 Genymotion Cloud SaaS、Microsoft Azure、Google Cloud Platform 或阿里云中执行类似的步骤。

1. 使用 [Genymotion AMI](https://aws.amazon.com/marketplace/seller-profile?id=933724b4-d35f-4266-905e-e52e4792bc45) 启动 EC2 实例

![AWS Genymotion AMI](https://user-images.githubusercontent.com/4301109/81505732-7bb3a100-92bf-11ea-9ba5-b1899810db2e.png)

2. 修改 AMI 的 **安全组** 以允许到端口 **5555** 的入站 TCP 连接。这是远程 adb 连接到 Genymotion Cloud VM 所必需的。

![允许 ADB 连接](https://user-images.githubusercontent.com/4301109/81505878-9b979480-92c0-11ea-9456-32cf5254d381.png)

3. 通过导航到 Genymotion Cloud VM 的公共 IP 来访问它。默认用户名是“genymotion”，密码是 EC2 实例 id。
[更多信息](https://docs.genymotion.com/paas/02_Getting_Started/021_AWS/)

4. 进入配置并启用 ADB

![在 Genymotion Cloud 中启用 ADB](https://user-images.githubusercontent.com/4301109/81505975-46a84e00-92c1-11ea-82a5-8912f96849b1.png)

5. 在本地计算机上，确保您可以通过 adb 连接到 Genymotion Cloud VM。

```bash
adb connect <public_ip>:5555
adb devices
```

![ADB 连接](https://user-images.githubusercontent.com/4301109/81506018-9be45f80-92c1-11ea-8486-fcac8daee7be.png)

6. 运行 MobSF docker 映像时，将环境变量“MOBSF_ANALYZER_IDENTIFIER”设置为“<public_ip>:5555”（示例：“3.81.202.69:5555”）。

7. 您现在可以在 AWS 中使用 Genymotion Cloud VM 执行 MobSF 动态分析。

## Corellium Android 虚拟机

?> 支持 **rooted userdebug** 构建，arm64 架构 Android **7.1.2 - 11.0**，最高 **API 30**

!> 您不得选择非 root **用户** 版本。 MobSF 需要 root **userdebug** 构建。

1. 创建受支持的 root **userdebug** Android 设备后，按照 Corellium 的“通过 VPN 连接”说明进行操作。

![Corellium Android](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/f384421c-98af-47b1-8d98-29641d9ca974)

2. 使用提供的 VPN 配置连接到 Corellium 网络。

3. 在本地运行 `adb connect` 以确保连接在您的主机上正常工作。

![Corellium adb](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/c6f1135e-b1ef-4a14-b9bf-6ebfab2e3cca)

4. 运行 MobSF docker 映像时，将环境变量“MOBSF_ANALYZER_IDENTIFIER”设置为“<private_ip_and_port>”（示例：“10.11.1.1:5001”）。

## Corellium iOS 虚拟机

从 MobSF v3.8.0 开始支持越狱的 Corellium iOS VM。
!> 未越狱的设备不能与 MobSF 一起使用。

1. 设置 Corellium 帐户后，从 https://app.corellium.com/profile/api 创建 API 密钥

2. 在环境变量`MOBSF_CORELLIUM_API_KEY`中设置API密钥

3. 要启用 MobSF HTTPs 代理，您必须在 iOS VM 中设置代理设置。转到iPhone“设置”->“Wi-Fi”->选择“Corellium”WiFi->向下滚动并选择“配置代理”->选择“手动配置”->将“服务器”设置为“127.0.0.1” ` 和 `Port` 为 `1337` -> 单击`保存`。

4. 运行 MobSF，现在您可以使用 Corellium 创建或管理越狱的 iOS VM。