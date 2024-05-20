# MobSF を実行する

?> MobSF を実行するには、[docker](https://docs.docker.com/get-docker/) がインストールされている必要があります。


## ダウンロード

最新のバージョン、機能、セキュリティ、バグ修正を入手するには、常に「最新」タグの付いた MobSF Docker イメージをダウンロードする必要があります。最新バージョンより後のバージョン付き [リリース](https://hub.docker.com/r/opensecurity/mobile-security-framework-mobsf/tags) も提供しています。

```
docker pull opensecurity/mobile-security-framework-mobsf:latest
```

＃＃ 走る

### 静的解析サポートを使用して MobSF を実行する

```
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

Web ブラウザで「http://127.0.0.1:8000」にある MobSF Web インターフェイスにアクセスできるようになりました。デフォルトの認証情報は「mobsf/mobsf」です。

## 静的および動的分析サポートを使用して MobSF を実行する

MobSF v3.6.9 以降の Docker イメージを使用して、静的分析と動的分析の両方をサポートして MobSF を実行することもできます。

!> MobSF を実行する前に、**[サポート対象](dynamic_analyzer.md)** Genymotion Android VM/Android Studio エミュレータのいずれかを実行する必要があります。続行する前に、[これ](dynamic_analyzer.md) をお読みください。

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_ANALYZER_IDENTIFIER=<adb device identifier> opensecurity/mobile-security-framework-mobsf:latest
```

?> MobSF は、**rooted** Android バージョン 4.1 ～ 11.0 (API 30 まで) での動的分析のみをサポートします。Android バージョン 12 以降はサポートされていません。


iOSの動的分析

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_CORELLIUM_API_KEY=<corellium api key> opensecurity/mobile-security-framework-mobsf:latest
```

より一般的な Docker オプションは、[MobSF Docker Options](docker.md) で利用できます。

## MobSFの使い方

Defcon Demo Labs 2020 のこのビデオでは、MobSF の基本機能のいくつかを説明しています。

<iframe width="760" height="515" src="https://www.youtube.com/embed/1NIQs82n3nw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### その他のリソース

* [過去のMobSFプレゼンテーションとスライド](https://mobsf.github.io/Mobile-Security-Framework-MobSF/presentations.html)
* [E ラーニング コース: MobSF による自動モバイル アプリケーション セキュリティ評価 -MAS](https://opsecx.com/index.php/product/automated-mobile-application-security-assessment-with-mobsf/)