# Frequently Asked Questions

## Database related exceptions when running Static Analysis

```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named 
```

### Solution

If you see exceptions like the one above, most probably it is because you have a newer version of MobSF with database scheme changes. See updating to perform database migration.


## Dynamic Analysis: APK Failed to Install


```
[INFO] 24/Sep/2020 13:50:56 - Installing APK
adb: failed to install C:/Users/XXXX/Mobile-Security-Framework-MobSF/uploads/xxxx/xxxx.apk: Failure [INSTALL_FAILED_NO_MATCHING_ABIS: Failed to extract native libraries, res=-113]
[ERROR] 24/Sep/2020 13:50:59 - This APK cannot be installed. Is this APK compatible the Android VM/Emulator?
```

```
[INFO] 24/Sep/2020 13:50:56 - Installing APK
adb: failed to install /x/xxx/xxx.apk: Failure [INSTALL_FAILED_MISSING_SHARED_LIBRARY: Package couldn't be installed in /data/app/com.xxx.xxx-1: Package com.xxx.xxxx requires unavailable shared library com.google.android.maps; failing!]
```

### Solution
The `INSTALL_FAILED_NO_MATCHING_ABIS` error is shown when you are trying to install an app that has native libraries which targets an unsupported architecture like ARM.
Genymotion or Android Studio Emulator x86 runs x86 or x86_64 architecture of Android and hence ARM libraries cannot work. So you need to provide the right APK targetting the right platform or use an ARM architecture based Android Studio Emulator for Dynamic Analysis.


You could make some ARM targetted apps work with Genymotion by using an ARM translation module. See [Genymotion ARM Translation](https://github.com/m9rco/Genymotion_ARM_Translation)
Sometimes you need Google Apps like the Playstore service for you app to run. In such cases, you will have to install the correct version of GApps for the Android version that you are using for dynamic analysis. See: [Open GApps](https://opengapps.org/)
