# Frequently Asked Questions

## Disable Authentication, I would like to run MobSF without authentication.

### Solution

Set environment variable `MOBSF_DISABLE_AUTHENTICATION=1` to disable Authentication and Authorization in MobSF. The REST APIs always requires the API Key. This cannot be disabled, however you can configure your own API key using the environment variable `MOBSF_SECRET_KEY`.

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


## Dynamic Analysis: MobSF docker in Linux host cannot talk with AVD/Genymotion in host

When you attempt to perform dynamic analysis with AVD or Genymotion emulator running in your Ubuntu or Linux based host, after running the docker image (`docker run -it --rm -e MOBSF_ANALYZER_IDENTIFIER=127.0.0.1:6555 -p 8000:8000 -p 1337:1337 opensecurity/mobile-security-framework-mobsf:latest`), you are seeing connectivity error messages such as `failed to connect to 'host.docker.internal:6555': Connection refused`.

### Solution
The `MOBSF_ANALYZER_IDENTIFIER` contains a localhost IP address. In order for the docker image to communicate correctly with the AVD or Genymotion running in the localhost, it need to use `host.docker.internal` to correctly route the traffic to the host operating system. In Linux based OS, this will not work out of the box. To fix this, first you need to ensure that your Docker version is `>=20.04`. Now run the MobSF docker image with the extra docker flags `--add-host=host.docker.internal:host-gateway`.
This should fix the network connectivity between adb inside the MobSF container and your AVD/Genymotion emulator in the Linux host running at a localhost IP.

Example: `docker run -it --rm -e MOBSF_ANALYZER_IDENTIFIER=127.0.0.1:6555 -p 8000:8000 -p 1337:1337 --add-host=host.docker.internal:host-gateway opensecurity/mobile-security-framework-mobsf:latest`
