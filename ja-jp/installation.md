
# <g1>インストール</g1>

!> MobSF を初めて使用する場合は、代わりに [簡単インストール](/ja-jp/mobsf_docker.md) を試してください。


## 従来の手順


**Windows 10, Ubuntu (18.04, 19.04) , macOS Catalinaで動作確認しています。**

!> [要件](/ja-jp/requirements.md)にて述べられたものがすべてインストール済であることを最初に確認してください。


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
