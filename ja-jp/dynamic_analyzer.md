# ダイナミックアナライザー

MobSF は、以下で作成された **特定** のルート化された Android VM/エミュレータをサポートしています。
* [Genymotion](https://www.genymotion.com/download/)
* [Genymotion クラウド VM](https://www.genymotion.com/pricing/)
* [Android Studio エミュレータ](https://developer.android.com/studio)
* [Corellium](https://support.corellium.com/getting-started/introduction-to-virtual-devices/quickstart-for-android)

## Genymotion アンドロイド
?> x86、x86_64 アーキテクチャ Android **4.1 ～ 11.0**、最大 **API 30** をサポート

Genymotion は、最小限の摩擦でセットアップできる推奨される動的解析環境です。 **MobSF を開始する前に、Genymotion Android VM を実行します。****Android 7.0** 以降を使用することをお勧めします。

* **Android 5.0 ～ 11.0** - これらのバージョンは **Frida** を使用し、設定やセットアップをしなくてもすぐに使用できます。
* **Android 4.1 ～ 4.4** - これらのバージョンは **Xused Framework** を使用しており、初めて動的分析の前にランタイムを MobSFy する必要があります。これらのバージョンでは、Xused モジュールのインストール後に VM を再起動する必要もあります。

Android VM を実行すると、タイトル バーからデバイス ID が表示されます。

![アナライザー識別子](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/6204cdf4-1bc6-4b9a-a9f6-99db64c2f8e2)

MobSF Docker イメージを実行するときに、環境変数 `MOBSF_ANALYZER_IDENTIFIER` を VM のデバイス識別子として設定します (例: `192.168.58.102:5555`)。

**HTTPS プロキシ**

* Android バージョン **4.4 ～ 11.0** の場合、グローバル プロキシ設定は実行時に自動的に適用されます。
* Android バージョン **4.1 ～ 4.3** の場合、Dynamic Analyzer ページに表示されているように Android VM プロキシを設定します。


## Android Studio エミュレータ
?> arm、arm64、x86、および x86_64 アーキテクチャ Android **5.0 ～ 9.0**、**API 28** までをサポート

Google Play ストアの Android エミュレータ イメージは製品イメージとみなされ、これらのイメージには root アクセス権がないため、MobSF では使用できません。

**Google Play ストアを使用せずに** Android 仮想デバイス (AVD) を作成します。

![Create AVD](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/28199a89-847a-411f-9f85-e1179b5f835a)

!> Android Studio IDE/AVD Manager UI から AVD を起動せず、以下の正確な手順に従ってください。

**エミュレータを使用してコマンドラインから AVD を実行します**

Android SDK エミュレータ ディレクトリを `PATH` 環境変数に追加します。

いくつかの場所の例

* Mac - `/Users/<user>/Library/Android/sdk/emulator`
* Linux - `/home/<user>/Android/Sdk/emulator`
* Windows - `C:\Users\<user>\AppData\Local\Android\Sdk\emulator`

**利用可能な Android 仮想デバイス (AVD) をリストします**


```bash
$ emulator -list-avds
Pixel_2_API_29
Pixel_3_API_28
Pixel_XL_API_24
Pixel_XL_API_25
```

!> **API 28** までの Android イメージのみがサポートされています。新しい Android AVD は書き込み可能な `/system` を提供していないため、MobSF では動作できません。


**Android 仮想デバイス (AVD) を実行**

「emulator」コマンド ライン オプションを使用して、**MobSF を開始する前に** AVD を実行します。

```bash
$ emulator -avd <non_production_avd_name> -writable-system -no-snapshot
```

![Android AVD](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/e9e849b6-69ad-47a4-8693-c75a0e1aa7cb)

エミュレータのシリアル番号を特定します。この例では、識別子は「emulator-5554」です。

MobSF Docker イメージを実行するときに、「MOBSF_ANALYZER_IDENTIFIER」を「emulator-5554」として設定します。

MobSF では、動的分析に AVD バージョン **5.0 ～ 9.0** が必要です。 **Android 7.0** 以降を使用することをお勧めします。

**HTTPS プロキシ**

* Android バージョン **5.0 ～ 9.0** の場合、グローバル プロキシ設定は実行時に自動的に適用されます。

**AVD 上の GApps (オプション)**

GApps が必要な場合は、<https://opengapps.org/> から適切なパッケージを見つけてください。

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

## Genymotion クラウド VM
?> x86、x86_64 アーキテクチャ Android **5.1 ～ 11.0**、**API 30** までをサポート

**MobSF を実行する前に、クラウドで Genymotion Android VM を実行します。Android 7.0** 以降を使用することをお勧めします。

このドキュメントでは、例としてアマゾン ウェブ サービス (AWS) を使用します。 Genymotion Cloud SaaS、Microsoft Azure、Google Cloud Platform、または Alibaba Cloud でも同様の手順に従う必要があります。

1. [Genymotion AMI](https://aws.amazon.com/marketplace/seller-profile?id=933724b4-d35f-4266-905e-e52e4792bc45) で EC2 インスタンスを起動します。

![AWS Genymotion AMI](https://user-images.githubusercontent.com/4301109/81505732-7bb3a100-92bf-11ea-9ba5-b1899810db2e.png)

2. AMI の **セキュリティ グループ**を変更して、ポート **5555** への受信 TCP 接続を許可します。これは、Genymotion Cloud VM へのリモート adb 接続に必要です。

![ADB 接続を許可](https://user-images.githubusercontent.com/4301109/81505878-9b979480-92c0-11ea-9456-32cf5254d381.png)

3. Genymotion Cloud VM のパブリック IP に移動して、Genymotion Cloud VM にアクセスします。デフォルトのユーザー名は「genymotion」、パスワードは EC2 インスタンス ID です。
[詳細情報](https://docs.genymotion.com/paas/02_Getting_Started/021_AWS/)

4. [設定] に移動し、ADB を有効にします。

![Genymotion Cloud で ADB を有効にする](https://user-images.githubusercontent.com/4301109/81505975-46a84e00-92c1-11ea-82a5-8912f96849b1.png)

5. ローカル マシンから、adb 経由で Genymotion Cloud VM に接続できることを確認します。

```bash
adb connect <public_ip>:5555
adb devices
```

![ADB 接続](https://user-images.githubusercontent.com/4301109/81506018-9be45f80-92c1-11ea-8486-fcac8daee7be.png)

6. MobSF Docker イメージを実行するときに、環境変数 `MOBSF_ANALYZER_IDENTIFIER` を `<public_ip>:5555` として設定します (例: `3.81.202.69:5555`)。

7. AWS の Genymotion Cloud VM を使用して MobSF 動的分析を実行できるようになりました。

## Corellium Android VM

?> **rooted userdebug** ビルド、arm64 アーキテクチャ Android **7.1.2 ～ 11.0**、**API 30** までをサポート

!> root 化されていない **user** ビルドを選択してはなりません。 MobSF には root 化された **userdebug** ビルドが必要です。

1. サポートされている root 化された **userdebug** Android デバイスを作成した後、Corellium の「VPN 経由で接続」の手順に従います。

![Corellium Android](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/f384421c-98af-47b1-8d98-29641d9ca974)

2. 提供された VPN 構成を使用して Corellium ネットワークに接続します。

3. ローカルで「adb connect」を実行して、ホストから接続が機能していることを確認します。

![Corellium adb](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/c6f1135e-b1ef-4a14-b9bf-6ebfab2e3cca)

4. MobSF Docker イメージを実行するときに、環境変数 `MOBSF_ANALYZER_IDENTIFIER` を `<private_ip_and_port>` として設定します (例: `10.11.1.1:5001`)。