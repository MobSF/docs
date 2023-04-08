# Instalación

!> Si es nuevo en MobSF, intente [instalación fácil](/es/mobsf_docker.md) en su lugar.


## Pasos heredados


**Probado en Windows 10, Ubuntu (18.04, 19.04) y macOS Catalina**

!> Se deben cumplir todos los [requisitos](/es/requirements.md) antes de intentar la instalación de MobSF.

## Linux/Mac

```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
./setup.sh
```

## Windows

```bash
git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF.git
cd Mobile-Security-Framework-MobSF
setup.bat
```

?> Los usuarios de Windows antes de ejecutar el archivo `setup.bat` deberán de cerrar todas las carpetas de MobSF o editores de texto con archivos del proyecto abiertos. Tener abierto cualquiera de los dos puede interrumpir la instalación causando errores de permisos.

# Ejecutar MobSF

## Linux o MacOS

```bash
./run.sh 127.0.0.1:8000
```

***

## Windows

```batch
run.bat 127.0.0.1:8000
```

!> MobSF escuchará la dirección `0.0.0.0:8000` si se usa el script sin ningún argumento.

En tu navegador web, visitar `http://localhost:8000/` para acceder a la interfaz web de MobSF
