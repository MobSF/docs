# Preguntas Frecuentes

## Excepciones relacionadas con la base de datos cuando se está ejecutando un Análisis Estático

```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named 
```

### Solución

Si se encuentra con excepciones como la mostrada anteriormente, es probable que se cuente con una versión más actualizada de MobSF que la indicada en el esquema de cambios de la base de datos. Para realizar una migración vea el apartado de [actualización](es-mx/updating.md)

## Análisis Dinámico: Instalación de APK falló

```
[INFO] 24/Sep/2020 13:50:56 - Installing APK
adb: failed to install C:/Users/XXXX/Mobile-Security-Framework-MobSF/uploads/xxxx/xxxx.apk: Failure [INSTALL_FAILED_NO_MATCHING_ABIS: Failed to extract native libraries, res=-113]
[ERROR] 24/Sep/2020 13:50:59 - This APK cannot be installed. Is this APK compatible the Android VM/Emulator?
```

```
[INFO] 24/Sep/2020 13:50:56 - Installing APK
adb: failed to install /x/xxx/xxx.apk: Failure [INSTALL_FAILED_MISSING_SHARED_LIBRARY: Package couldn't be installed in /data/app/com.xxx.xxx-1: Package com.xxx.xxxx requires unavailable shared library com.google.android.maps; failing!]
```

### Solución

El error `INSTALL_FAILED_NO_MATCHING_ABIS` ocurre cuando se está tratando instalar una aplicación que tiene dependencias nativas que dependen de arquitecturas sin soporte, como lo es ARM.
Genymotion o Android Studio Emulator x86 ejecuta arquitecturas x86 o x86_64 de Andorid, por ello librerías de ARM no pueden funcionar. Se deberá de porveer el APK correcto o usar un emulador basado en ARM para el Análisis Dinámico.

Se podría lograr que funcionaran algunas aplicaciónes diseñadas para ARM con Genymotion usando el modulo de traducción de ARM. Para más información consultar [Genymotion ARM Translation](https://github.com/m9rco/Genymotion_ARM_Translation).
En ocasiones se podría llegar a necesitar aplicaciónes de Google, como el PlayStore Service, para que la aplicación funcione de manera correcta. En dichos casos se deberá de instalar la versión correcta de las GApps para la versión de Android que se está usando para análisis dinámico. Más información en [Open GApps](https://opengapps.org/).