# Analizador dinámico

MobSF es compatible con **ciertas** máquinas virtuales/emuladores de Android rooteados creados con:
* [Genymotion](https://www.genymotion.com/download/)
* [Máquina virtual en la nube de Genymotion](https://www.genymotion.com/pricing/)
* [Emulador de Android Studio](https://developer.android.com/studio)
* [Corellium](https://support.corellium.com/getting-started/introduction-to-virtual-devices/quickstart-for-android)

* MobSF también admite dispositivos virtuales iOS con jailbreak creados con Corellium

## Genymotion Android
?> Compatible con arquitectura x86, x86_64 Android **4.1 - 11.0**, hasta **API 30**

Genymotion es el entorno de análisis dinámico preferido que puede configurar con la menor fricción. Ejecute una máquina virtual Android Genymotion **antes de iniciar MobSF.** Recomendamos usar **Android 7.0** y superior.

* **Android 5.0 - 11.0**: estas versiones usan **Frida** y funcionan de manera inmediata sin necesidad de configuración o instalación.
* **Android 4.1 - 4.4**: estas versiones usan **Xposed Framework** y requieren MobSFy el tiempo de ejecución antes de Dynamic Analysis por primera vez. Estas versiones también requieren el reinicio de la máquina virtual después de instalar los módulos Xposed.

Después de ejecutar Android VM, puede ver el identificador del dispositivo en la barra de título.


![Identificador del analizador](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/6204cdf4-1bc6-4b9a-a9f6-99db64c2f8e2)

Establezca la variable de entorno `MOBSF_ANALYZER_IDENTIFIER` como el identificador del dispositivo de la VM cuando ejecute la imagen acoplable de MobSF (Ejemplo: `192.168.58.102:5555`).

**Proxy HTTPS**

* Para las versiones de Android **4.4 - 11.0**, la configuración del proxy global se aplica automáticamente en tiempo de ejecución.
* Para la versión de Android **4.1 - 4.3**, configure el proxy de VM de Android como se muestra en la página Dynamic Analyzer.

## Emulador de Android Studio
?> Admite la arquitectura arm, arm64, x86 y x86_64 Android **5.0 - 9.0**, hasta **API 28**

La imagen del emulador de Android con Google Play Store se considera una imagen de producción y no puede usarla con MobSF ya que esas imágenes no tienen acceso de root.

Cree un dispositivo virtual Android (AVD) **sin Google Play Store**.

![Create AVD](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/28199a89-847a-411f-9f85-e1179b5f835a)

!> No inicie el AVD desde Android Studio IDE/AVD Manager UI, en su lugar, siga las instrucciones exactas a continuación.


**Ejecute AVD desde la línea de comandos usando el emulador**

Agregue su directorio de emulador de SDK de Android a la variable de entorno `PATH`.

Algunas ubicaciones de ejemplo

* Mac - `/Users/<user>/Library/Android/sdk/emulator`
* Linux - `/home/<user>/Android/Sdk/emulator`
* Windows - `C:\Users\<user>\AppData\Local\Android\Sdk\emulator`

**Lista de dispositivos virtuales Android disponibles (AVD)**

```bash
$ emulator -list-avds
Pixel_2_API_29
Pixel_3_API_28
Pixel_XL_API_24
Pixel_XL_API_25
```

!> ¡Solo se admiten imágenes de Android hasta **API 28**! Los AVD de Android más nuevos no ofrecen un "/ sistema" grabable y, por lo tanto, no pueden funcionar con MobSF.

**Ejecutar dispositivo virtual Android (AVD)**

Ejecute un AVD **antes de iniciar MobSF** utilizando las opciones de la línea de comandos `emulator`.

```bash
$ emulator -avd <non_production_avd_name> -writable-system -no-snapshot
```

![Android AVD](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/e9e849b6-69ad-47a4-8693-c75a0e1aa7cb)

Identifique el número de serie del emulador. En este ejemplo, el identificador es `emulator-5554`.

Establezca `MOBSF_ANALYZER_IDENTIFIER` como `emulator-5554` cuando ejecute la imagen acoplable de MobSF.

MobSF requiere la versión AVD **5.0 a 9.0** para el análisis dinámico. Recomendamos usar **Android 7.0** y superior.

**Proxy HTTPS**

* Para las versiones de Android **5.0 - 9.0**, la configuración del proxy global se aplica automáticamente en tiempo de ejecución.

**GApps en AVD (opcional)**

Si necesita GApps, busque el paquete adecuado en <https://opengapps.org/>

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

## Máquina virtual en la nube Genymotion
?> Compatible con arquitectura x86, x86_64 Android **5.1 - 11.0**, hasta **API 30**

Ejecute una máquina virtual Android Genymotion en la nube **antes de ejecutar MobSF.** Recomendamos usar **Android 7.0** y superior.

Esta documentación utiliza Amazon Web Services (AWS) como ejemplo. Debe seguir pasos similares en Genymotion Cloud SaaS, Microsoft Azure, Google Cloud Platform o Alibaba Cloud.

1. Inicie una instancia EC2 con [Genymotion AMI](https://aws.amazon.com/marketplace/seller-profile?id=933724b4-d35f-4266-905e-e52e4792bc45)

![AWS Genymotion AMI](https://user-images.githubusercontent.com/4301109/81505732-7bb3a100-92bf-11ea-9ba5-b1899810db2e.png)

2. Modifique el **Grupo de seguridad** de la AMI para permitir conexiones TCP entrantes al puerto **5555**. Esto es necesario para la conexión adb remota a Genymotion Cloud VM.

![Permitir conexión ADB](https://user-images.githubusercontent.com/4301109/81505878-9b979480-92c0-11ea-9456-32cf5254d381.png)

3. Acceda a Genymotion Cloud VM navegando a su IP pública. El nombre de usuario predeterminado es `genymotion` y la contraseña es ID de instancia de EC2.
[Más información](https://docs.genymotion.com/paas/02_Getting_Started/021_AWS/)

4. Vaya a Configuración y habilite ADB

![Habilitar ADB en Genymotion Cloud](https://user-images.githubusercontent.com/4301109/81505975-46a84e00-92c1-11ea-82a5-8912f96849b1.png)

5. Desde su máquina local, asegúrese de poder conectarse a Genymotion Cloud VM a través de adb.


```bash
adb connect <public_ip>:5555
adb devices
```

![Conexión ADB](https://user-images.githubusercontent.com/4301109/81506018-9be45f80-92c1-11ea-8486-fcac8daee7be.png)

6. Configure la variable de entorno `MOBSF_ANALYZER_IDENTIFIER` como `<public_ip>:5555` cuando ejecute la imagen acoplable de MobSF (Ejemplo: `3.81.202.69:5555`).

7. Ahora puede realizar un análisis dinámico de MobSF con Genymotion Cloud VM en AWS.

## Máquina virtual de Android Corellium

?> Admite compilaciones **rooted userdebug**, arquitectura arm64 Android **7.1.2 - 11.0**, hasta **API 30**

!> No debe elegir compilaciones de **usuario** no rooteados. MobSF requiere compilaciones rooteadas **userdebug**.

1. Después de crear un dispositivo Android arraigado **userdebug** compatible, siga las instrucciones de Corellium `Conectar a través de VPN`.

![Corellium Android](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/f384421c-98af-47b1-8d98-29641d9ca974)

2. Conéctese a la red de Corellium utilizando la configuración de VPN proporcionada.

3. Ejecute `adb connect` localmente para asegurarse de que la conexión funcione desde su host.

![Adb de Corellium](https://github.com/MobSF/Mobile-Security-Framework-MobSF/assets/4301109/c6f1135e-b1ef-4a14-b9bf-6ebfab2e3cca)

4. Configure la variable de entorno `MOBSF_ANALYZER_IDENTIFIER` como `<private_ip_and_port>` cuando ejecute la imagen acoplable de MobSF (Ejemplo: `10.11.1.1:5001`).

## Máquina virtual Corellium iOS

Admite máquinas virtuales Corellium iOS con jailbreak desde MobSF v3.8.0 en adelante.
!> Los dispositivos sin jailbreak no se pueden utilizar con MobSF.

1. Después de configurar la cuenta de Corellium, cree una clave API desde https://app.corellium.com/profile/api

2. Establezca la clave API en la variable de entorno `MOBSF_CORELLIUM_API_KEY`

3. Para habilitar el proxy HTTPs de MobSF, deberá configurar la configuración del proxy en la máquina virtual iOS. Vaya a iPhone `Configuración` -> `Wi-Fi` -> Elija `Corellium` WiFi -> Desplácese hacia abajo y elija `Configurar Proxy` -> Elija `Configuración manual` -> Configure el `Servidor` como `127.0.0.1 ` y `Puerto` como `1337` -> Haga clic en `Guardar`.

4. Ejecute MobSF y ahora podrá crear o administrar máquinas virtuales iOS con jailbreak con Corellium.
