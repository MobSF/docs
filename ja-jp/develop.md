
# 要件

## 静的解析
* **Mac**
   * [Git](https://www.atlassian.com/git/tutorials/install-git)のインストール
   * [Python **3.8-3.9**](https://www.python.org/)のインストール
   * Python 3.8以上をインストール後 `/Applications/Python 3.8/`に移動して最初に`Update Shell Profile.command`を実行後、`Install Certificates.command`を実行
   * [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)のインストール
   * `xcode-select --install`でコマンドラインツールを導入
   * [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) を、[wikiの説明](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)に従ってダウンロードしてインストール
   * Windowsアプリの静的解析をMacおよびLinuxで行うにはWindowsホストまたはWindows VMが必要です。[詳細](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md)


* **Ubuntu/DebianベースのLinux**:
   * Gitのインストール`sudo apt-get install git`
   * Python **3.8-3.9**のインストール `sudo apt-get install python3.8`
   * JDK 8+ のインストール`sudo apt-get install openjdk-8-jdk`
   * 以下の依存関係をインストール
      ```bash
      sudo apt install python3-dev python3-venv python3-pip build-essential libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg8-dev zlib1g-dev wkhtmltopdf
      ```
   * Windowsアプリの静的解析をMacおよびLinuxで行うにはWindowsホストまたはWindows VMが必要です。[詳細](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/mobsf/install/windows/readme.md)

* **Windows**
   * [Git](https://git-scm.com/download/win)のインストール
   * [Python **3.8-3.9**](https://www.python.org/)のインストール
   * [JDK 8+](https://www3.ntu.edu.sg/home/ehchua/programming/howto/JDK_Howto.html)のインストール
   * [Microsoft Visual C++ ビルドツール](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=16)のインストール
   * [OpenSSL (light 版以外)](https://slproweb.com/products/Win32OpenSSL.html)のインストール
   * [wkhtmltopdf](https://wkhtmltopdf.org/downloads.html) を、[wikiの説明](https://github.com/JazzCore/python-pdfkit/wiki/Installing-wkhtmltopdf)に従ってダウンロードしてインストール
   * `wkhtmltopdf`バイナリを含むフォルダをPATH環境変数に追加してください。


?> **重要:**`JAVA_HOME` 環境変数を実行してください。iOS IPA解析は**Mac、LinuxおよびDockerコンテナ**でのみ動作します。

***
## 動的解析
* **動的解析は、MobSF dockerコンテナ利用時、あるいはMobSFをVM上で実行しているときには動作しません。**
* [Genymotion](https://www.genymotion.com/fun-zone/)か[Genymotion Cloud VM](https://www.genymotion.com/cloud/)、または[Android Studio Emulator](https://developer.android.com/studio)をインストールしてください。



# <g1>インストール</g1>


**Windows 10, Ubuntu (18.04, 19.04) , macOS Catalinaで動作確認しています。**

!> 要件にて述べられたものがすべてインストール済であることを最初に確認してください。


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

?> Windowsユーザーの場合、`setup.bat`を実行する前にMobSF以下のすべてのフォルダおよびテキストエディタを閉じておいてください。このどちらかの場合、権限エラーでセットアップが中断されることがあります。


# <g1>MobSFの実行</g1>

## Linux/Mac
```bash
./run.sh 127.0.0.1:8000
```

***

## Windows

```batch
run.bat 127.0.0.1:8000
```

!> MobSF はスクリプトに引数で指定しない限り `0.0.0.0:8000`をリッスンします。

ブラウザにて `http://localhost:8000/` に遷移することでMobSFのWebインタフェースにアクセスできます。

# 動的解析

## Genymotion Android
?> x86, x86_64アーキテクチャのAndroid **4.1 - 11.0**、**API 30**までをサポートしています。

Genymotionは、手間を最小限に抑えて設定できる最適な動的解析環境です。Genymotion Android VMを**MobSFを実行する前に**実行してください。すべては実行時に自動的に設定されます。**Android 7.0**以上の利用を推奨します。

* **Android 5.0 - 11.0** - これらのバージョンは**Frida**を利用しており、設定やセットアップなしで箱だしで利用できます。
* **Android 4.1 - 4.4** - これらのバージョンは**Xposed Framework**を利用しており、動的解析の最初の実行前にランタイムをMobSF化する必要があります。これらのバージョンでは、Xposed Moduleを導入したあとにVMを再起動する必要があります。

「動的解析」ページの **MobSFy Android Runtime (AndroidランタイムのMobSF化)** ボタンをクリックすることでAndroidランタイム環境をMobSF化できます。

![MobSF化](https://user-images.githubusercontent.com/4301109/77839885-11033780-714f-11ea-9d52-df7b0bd314a0.png)

**HTTPS Proxy**

* Androidバージョン**4.4 - 11.0**では、グローバルなプロキシ設定が自動的にランタイムに適用されます。
* Androidバージョン**4.1 - 4.3**では、Android VMプロキシを「動的解析」ページに表示されているように設定してください。

もし「動的解析」画面でAndroidデバイスが検知されなかった場合、`ANALYZER_IDENTIFIER` を`<user_home_dir>/.MobSF/config.py` または環境変数 `ANALYZER_IDENTIFIER` にて手動で設定する必要があります。

例: `ANALYZER_IDENTIFIER = '192.168.56.101:5555'`
AndroidデバイスのIPはGenymotionのタイトルバーに記載されています。デフォルトポートは`5555`です。

![動的解析IP](https://user-images.githubusercontent.com/4301109/65379210-0b312300-dce2-11e9-8827-f63d3b95dfd1.png)

## Android Studioエミュレータ
?> arm, arm64, x86, x86_64アーキテクチャのAndroid **5.0 - 9.0**、**API 28**までをサポートしています。

Google Play StoreありのAndroidエミュレータイメージはプロダクションイメージとされており、MobSFで用いることはできません。
**Google Play Storeなしの** Android Virtual Device (AVD) を作成してください。AVDはAndroid Studioから起動するのではなく、 `emulator` コマンドラインオプションで書き込み可能なシステムでAVDを起動してください。

そのために、Android SDKのemulator ディレクトリを `PATH` に追加してください。

いくつかの場所の例

* Mac - `/Users/<user>/Library/Android/sdk/emulator`
* Linux - `/home/<user>/Android/Sdk/emulator`
* Windows - `C:\Users\<user>\AppData\Local\Android\Sdk\emulator`

**利用可能なAndroid Virtual Devices (AVD) のリスト**

```bash
$ emulator -list-avds
Pixel_2_API_29
Pixel_3_API_28
Pixel_XL_API_24
Pixel_XL_API_25
```

!>**API 28** までのAndroidイメージのみがサポートされています！


`ADB_BINARY` パスを `<user_home_dir>/.MobSF/config.py` に指定します。

Android Studioに付属のadbバイナリを使用していることを確認してください。異なるバージョンを使用すると、競合が発生し、動的解析中に問題が発生する可能性があります。

いくつかの場所の例

```python
ADB_BINARY = '/Users/<user>/Library/Android/sdk/platform-tools/adb' # Mac
ADB_BINARY = '/home/<user>/Android/Sdk/platform-tools/adb' # Linux
ADB_BINARY = 'C:\\Users\\<user>\\AppData\\Local\\Android\\Sdk\\platform-tools\\adb.exe' # Windows
ADB_BINARY = 'C:/Users/<user>/AppData/Local/Android/sdk/platform-tools/adb.exe' # Windows
```

**Android Virtual Device (AVD) の実行**

**MobSFの起動前に** AVDを `emulator` コマンドラインオプションを用いて起動してください。

```bash
$ emulator -avd <non_production_avd_name> -writable-system -no-snapshot
```

すべては実行時に自動的に設定されます。MobSFは動的解析にAVDバージョン **5.0 ～ 9.0** を要求します。**Android 7.0**以上の利用を推奨します。

**HTTPS Proxy**

* Androidバージョン**5.0- 9.0**では、グローバルなプロキシ設定が自動的にランタイムに適用されます。

**AVDにGAppsを導入 (オプション)**

GAppsが必要な場合は、<https://opengapps.org/>から適切なパッケージを探します。

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
?> x86, x86_64アーキテクチャのAndroid **5.1 - 11.0**、**API 30**までをサポートしています。

クラウドのGenymotion Android VMを**MobSFを実行する前に**実行し、adbコマンドで接続してください。すべては実行時に自動的に設定されます。**Android 7.0**以上の利用を推奨します。

このドキュメントでは、例としてAmazon Web Services(AWS)を使用します。Genymotion Cloud SaaS、Microsoft Azure、Google Cloud Platform、またはAlibaba Cloudでも同様の手順を踏む必要があります。

1. [Genymotion AMI](https://aws.amazon.com/marketplace/seller-profile?id=933724b4-d35f-4266-905e-e52e4792bc45)でEC2インスタンスを起動します。

![AWS Genymotion AMI](https://user-images.githubusercontent.com/4301109/81505732-7bb3a100-92bf-11ea-9ba5-b1899810db2e.png)

2. AMIの**Security Group**を変更して、ポート**5555**へのインバウンドTCP接続を許可します。これは、Genymotion Cloud VMへのリモートadb接続に必要です。

![ADBの接続許可](https://user-images.githubusercontent.com/4301109/81505878-9b979480-92c0-11ea-9456-32cf5254d381.png)

3. パブリックIPを用いて、Genymotion Cloud VMにアクセスします。デフォルトのユーザー名は`genymotion`で、パスワードはEC2インスタンスIDです。
   [詳細](https://docs.genymotion.com/paas/8.0/02_Getting_Started/021_AWS.html#create-and-set-up-an-instance)

4. 「Configuration」に移動してADBを有効化（Enable）します。

![Genymotion CloudにてADBを有効化](https://user-images.githubusercontent.com/4301109/81505975-46a84e00-92c1-11ea-82a5-8912f96849b1.png)

5. ローカルのマシンから、Genymotion Cloud VMにadbで接続できることを確認してください。

```bash
adb connect <public_ip>:5555
adb devices
```
![ADB connect](https://user-images.githubusercontent.com/4301109/81506018-9be45f80-92c1-11ea-8486-fcac8daee7be.png)

6. これでMobSF動的解析をAWS上のGenymotion Cloud VMで実施できるようになりました。

もし「動的解析」画面でクラウドVMが検知されなかった場合、`ANALYZER_IDENTIFIER` を`<user_home_dir>/.MobSF/config.py` または環境変数 `ANALYZER_IDENTIFIER` にて手動で設定する必要があります。

例: `ANALYZER_IDENTIFIER = '<public_ip>:5555'`.

もしMobSFがadbコマンドを見つけられなかった場合、`ADB_BINARY` を `<user_home_dir>/.MobSF/config.py`にて設定する必要があります。

例: `ADB_BINARY = '/Applications/Genymotion.app/Contents/MacOS/tools/adb'`.

# MobSFの更新

MobSFを更新する場合、ほとんどの場合、データベースの移行を実行する必要があります。そうしないと、次のようなエラーが表示されます。
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

!>上記でうまくいかない場合は、`~/.MobSF` または `C:\Users\<user>\.MobSF` を削除して、`setup.sh` または `setup.bat` を再度実行する必要があるかもしれませんが、これは以前のスキャン結果を削除します。

# テストの実行
テストの実行にはtoxを使用します。virtualenv外でtoxをインストールしてください。
```bash
pip install tox
```

**lintの実行**
```bash
tox -e lint
```

**lintとテストの実行**
```bash
tox -e lint,test
```

