
# 要件

!> [簡易インストール](/zh-cn/mobsf_docker.md)を行っている場合は不要です。


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

