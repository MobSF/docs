# FAQ (よくある質問とその答え)

## 静的解析実行時のデータベース関連の例外

```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named
```

### 解決策

この例外が起きるのは、ほとんどの場合新しいバージョンのMobSFにてデータベーススキーマが変更されたことによります。[MobSFの更新](/ja-jp/updating.md)を参照してデータベースのマイグレーションを行ってください。


## 動的解析: APKインストールの失敗


```
[INFO] 24/Sep/2020 13:50:56 - Installing APK
adb: failed to install C:/Users/XXXX/Mobile-Security-Framework-MobSF/uploads/xxxx/xxxx.apk: Failure [INSTALL_FAILED_NO_MATCHING_ABIS: Failed to extract native libraries, res=-113]
[ERROR] 24/Sep/2020 13:50:59 - This APK cannot be installed. Is this APK compatible the Android VM/Emulator?
```

```
[INFO] 24/Sep/2020 13:50:56 - Installing APK
adb: failed to install /x/xxx/xxx.apk: Failure [INSTALL_FAILED_MISSING_SHARED_LIBRARY: Package couldn't be installed in /data/app/com.xxx.xxx-1: Package com.xxx.xxxx requires unavailable shared library com.google.android.maps; failing!]
```

### 解決策
`INSTALL_FAILED_NO_MATCHING_ABIS` エラーは、サポートされていないアーキテクチャ、例えばARMをターゲットとしてネイティブライブラリを含んだアプリをインストールしようとしたときに生じます。
GenymotionまたはAndroid Studio Emulator x86はAndroidのx86またはx86_64アーキテクチャで動作していますのd、絵ARMライブラリは動作しません。プラットフォームに応じた適切なAPKを利用するか、動的解析にはARMベースのAndroid Studio Emulatorを用いてください。


ARMをターゲットとしたアプリを「ARM変換モジュール」を用いることでGenymotionで動かすことができるかもしれません。[Genymotion ARM Translation](https://github.com/m9rco/Genymotion_ARM_Translation)を参照してください
場合によってはアプリを実行するためにはPlaystoreサービスのようなGoogle Appsが必要になることもあります。このような場合は、Androidバージョンに見合った適切なバージョンのGAppsを導入し、それを動的解析に使う必要があります。[Open GApps](https://opengapps.org/)を参照してください。
