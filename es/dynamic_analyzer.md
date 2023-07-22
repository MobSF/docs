# Analizador Dinámico

!> Para el análisis dinámico es posible usar un dispositivo móvil real, pero **no tiene soporte de manera oficial**. 

## Genymotion Android

?> Tiene soporte para las arquitecturas x86, x86_64 de Android **4.1 - 11.0**, hasta la versión **30 del API**.

El ambiente preferido para el análisis dinámico es Genymotion, dado a que se puede configurar de manera sencilla. Se debe de asegurar que una máquina virtual de Genymotion Android esté corriendo **antes de inicializar MobSF**. Todo se configurará de manera automática en tiempo de ejecución. Recomendamos usar **Android 7.0** o superior.

* **Android 5.0 - 11.0** - Estas versiones usan **Frida** y funcionan de inmediato sin necesidad de configuraciones adicionales.
* **Android 4.1 - 4.4** - Estas versiones usan **Xposed Framework** y requieren que se use MobSF en el tiempo de ejecución (runtime) previo a usar el Analizador Dinámico por primera vez. Así mismo, estás versiones necesitan que la Máquina Virtual se reinicie después de instalar Xposed Modules.

Haz clic en el botón **MobSFy Android Runtime** en la página del Analizador Dinámico para correr MobSF en el entorno de ejecución de Android.

![MobSFy](https://user-images.githubusercontent.com/4301109/77839885-11033780-714f-11ea-9d52-df7b0bd314a0.png)

**Proxys con HTTPS**

* Para las versiones de Android **4.4 - 11.0**, las configuraciónes globales del proxy son aplicadas automáticamente al tiempo de ejecución.
* Para las versiones de Android **4.1 - 4.3**, configurar el proxy de la Máquina Virtual de Andoid como se muestra en la página del Analizador Dinámico.

En dado caso que el Analizador Dinámico no detecte el dispositivo Android, se deberá de configurar de manera manual el `ANALYZER_IDENTIFIER` dentro de `<user_home_dir>/.MobSF/config.py` o por medio de la variable de ambiente `ANALYZER_IDENTIFIER`.

Ejemplo: `ANALYZER_IDENTIFIER = '192.168.56.101:5555'`.
Se puede encontrar la dirección IP del dispositivo desde Genymotion, y su puerto default es el `5555`.

![IP del Analizador Dinámico](https://user-images.githubusercontent.com/4301109/65379210-0b312300-dce2-11e9-8827-f63d3b95dfd1.png)

## Emulador de Android Studio

?> Tiene soporte para las arquitecturas x86, x86_64 de Android **5.0 - 9.0**, hasta la versión **28 del API**.

La imagen del emulador de Android con Google Play Store está considerada como una imagen de producción, por ello no se puede usar MobSF con ella.
Se necesita crear un Dispositivo Android Virtual (AVD) **sin Google Play Store**. No inicies el AVD desde Android Studio, en su lugar inícialo desde la terminal usando la opción `emulador`.

Se necesita crear un Dispositivo Andorid Virtual (AVD) **sin la Google Play Store**. No se debe incializar el AVD desde Android Studio, en su lugar iniciar el AVD con la terminal usando la opción `emulador`. Para ello se debe de añadir el directorio del emulador del SDK a `PATH`. Algunos directorios donde se puede encontrar el emulador son:

* Mac - `/Users/<user>/Library/Android/sdk/emulator`
* Linux - `/home/<user>/Android/Sdk/emulator`
* Windows - `C:\Users\<user>\AppData\Local\Android\Sdk\emulator`

**Enlistar los Dispositivos Android Virtuales (AVD)**

```bash
$ emulator -list-avds
Pixel_2_API_29
Pixel_3_API_28
Pixel_XL_API_24
Pixel_XL_API_25
```

!> Solo las imagenes hasta la versión **28 del API** de Android están soportadas.

Se debe de configurar la ruta `ADB_BINARY` dentro de `<user_home_dir>/.MobSF/config.py` y asegurarse de que se está usando el binario ADB que viene incluido con Android Studio. Si es necesario utilizar una versión diferente a esta pueden llegar a ocurrir conflictos y errores al momento de intentar un análisis dinámico.

Algunos ejemplos de las rutas del binario ADB son:

```python
ADB_BINARY = '/Users/<user>/Library/Android/sdk/platform-tools/adb' # Mac
ADB_BINARY = '/home/<user>/Android/Sdk/platform-tools/adb' # Linux
ADB_BINARY = 'C:\\Users\\<user>\\AppData\\Local\\Android\\Sdk\\platform-tools\\adb.exe' # Windows
ADB_BINARY = 'C:/Users/<user>/AppData/Local/Android/sdk/platform-tools/adb.exe' # Windows
```

**Ejecutar el Dispositivo Android Virtual (AVD)**

Se debe de ejecutar el AVD **antes de inicializar MobSF** usando la opción `emulator` en la terminal.

```bash
$ emulator -avd <nombre_del_avd> -writable-system -no-snapshot
```

Todo se configurará de manera automatica durante el tiempo de ejecución. MobSF requiere una versión **5.0 a 9.0** de AVD para el análisis dinámico. Es recomendable usar **Android 7.0** o superior.

**Proxy HTTPS**

* Para versiones de Android **5.0 a 9.0** las configuraciónes globales de los proxy son aplicadas de manera automática durante el tiempo de ejecución.

**GApps on AVD (Optional)**

Si se necesitan GApps, se pueden encontrar los paquetes apropiados en <https://opengapps.org/>

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
?> Soporte para las arquitecturas x86, x86_64 de Android **5.1 a 11.0** y hasta el **API 30**

Run a Genymotion Android VM in cloud and connect to it via adb **before starting MobSF.** Everything will be configured automatically at runtime. We recommend using **Android 7.0** and above.

Se debe ejecutar una máquina virtual de Genymotion Android en la nube y conectarse a ella vía ADB **antes de inicializar MobSF**. Todo se configurará de manera automática durante el tiempo de ejecución. **Android 7.0 o superior** es recomendado para este caso de uso.

Esta documentación usa de ejemplo a Amazon Web Services (AWS), pero se necesitará seguir pasos similares en otras nubes como Genymotion Cloud SaaS, Microsoft Azure, Google Cloud Platform o Alibaba Cloud.

1. Inicia una intancia de EC2 con [Genymotion AMI](https://aws.amazon.com/marketplace/seller-profile?id=933724b4-d35f-4266-905e-e52e4792bc45)

![AWS Genymotion AMI](https://user-images.githubusercontent.com/4301109/81505732-7bb3a100-92bf-11ea-9ba5-b1899810db2e.png)

2. Modifica el **Grupo de Seguridad** (Security Group) de la AMI para permitir conecciónes TCP entrantes al puerto **5555**. Esto es un requerimiento para establecer la conección remota ADB a la máquina virtual de Genymotion Cloud.

![ADB Connection](https://user-images.githubusercontent.com/4301109/81505878-9b979480-92c0-11ea-9456-32cf5254d381.png)

3. Accede a la máquina virtual de Genymotion Cloud navegando a la IP pública. El usuario por defecto es `genymotion` y la contraseña es el ID de la instancia de EC2. [Más información](https://docs.genymotion.com/paas/8.0/02_Getting_Started/021_AWS.html#create-and-set-up-an-instance).

4. Navega a la configuración y habilita ADB.

![ADB en Genymotion Cloud](https://user-images.githubusercontent.com/4301109/81505975-46a84e00-92c1-11ea-82a5-8912f96849b1.png)

5. Probar la conexión a la máquina virtual de Genymotion Cloud de manera local por medio de ADB.

```bash
adb connect <ip_pública>:5555
adb devices
```

![ADB](https://user-images.githubusercontent.com/4301109/81506018-9be45f80-92c1-11ea-8486-fcac8daee7be.png)

6. MobSF está listo para realizar un análisis dinámico con Genymotion Cloud.

Si el Analizador Dinámico no es detectado por la máquina virtual en la nube, se deberá deconfigurar de manera manual  `ANALYZER_IDENTIFIER` en `<directorio_home_del_usuario>/.MobSF/config.py` o por medio de la variable de ambiente `ANALYZER_IDENTIFIER`.

Ejemplo: `ANALYZER_IDENTIFIER = '<ip_pública>:5555'`.

Si MobSF no puede detectar el ADB se deberá de configurar el `ADB_BINARY` en `<directorio_home_del_usuario>/.MobSF/config.py`.

Ejemplo: `ADB_BINARY = '/Applications/Genymotion.app/Contents/MacOS/tools/adb'`.
