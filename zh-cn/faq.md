# 常见问题

## 当执行静态分析时遇到数据库异常 Database related exceptions when running Static Analysis

```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named 
```

### 解决方式

如果您看到上述异常，则很可能是因为你有一个MobSF数据库Scheme的较新版本。请参考 更新 以执行数据库迁移。


## 动态分析：APK无法安装


```
[INFO] 24/Sep/2020 13:50:56 - Installing APK
adb: failed to install C:/Users/XXXX/Mobile-Security-Framework-MobSF/uploads/xxxx/xxxx.apk: Failure [INSTALL_FAILED_NO_MATCHING_ABIS: Failed to extract native libraries, res=-113]
[ERROR] 24/Sep/2020 13:50:59 - This APK cannot be installed. Is this APK compatible the Android VM/Emulator?
```

```
[INFO] 24/Sep/2020 13:50:56 - Installing APK
adb: failed to install /x/xxx/xxx.apk: Failure [INSTALL_FAILED_MISSING_SHARED_LIBRARY: Package couldn't be installed in /data/app/com.xxx.xxx-1: Package com.xxx.xxxx requires unavailable shared library com.google.android.maps; failing!]
```

### 解决方式

当你尝试安装App时，显示`INSTALL_FAILED_NO_MATCHING_ABIS`错误，不受支持的架构，如ARM。
Genymotion或Android Studio模拟器x86运行Android的x86或x86_64架构，因此ARM库无法工作。因此，你需要提供针对对应平台的架构Apk或使用基于ARM体系结构的Android Studio模拟器进行动态分析。


你可以通过使用ARM转换模块使某些以ARM为目标的应用程序与Genymotion一起使用。参见[Genymotion ARM翻译]（https://github.com/m9rco/Genymotion_ARM_Translation）
有时，你需要运行Playstore服务之类的Google Apps才能运行该应用。在这种情况下，你必须将为用于动态分析的Android版本安装正确版本的GApp。请参阅：[Open GApps]（https://opengapps.org/）
