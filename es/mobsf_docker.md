# Ejecutando MobSF

?> Debe tener [docker](https://docs.docker.com/get-docker/) instalado para ejecutar MobSF.


## Descargar

Siempre debe descargar la imagen acoplable de MobSF etiquetada como "más reciente" para obtener la versión, las características, la seguridad y las correcciones de errores más actualizadas. También ofrecemos [lanzamientos](https://hub.docker.com/r/opensecurity/mobile-security-framework-mobsf/tags) versionados que están detrás de la última versión.

```
docker pull opensecurity/mobile-security-framework-mobsf:latest
```

## Correr

### Ejecute MobSF con soporte de análisis estático

```
docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest
```

### Ejecute MobSF con soporte de análisis estático y dinámico

También puede ejecutar MobSF con soporte de análisis estático y dinámico utilizando la imagen acoplable de MobSF v3.6.9 en adelante.

!> Debe ejecutar cualquiera de los **[compatibles](dynamic_analyzer.md)** Genymotion Android VM/Android Studio Emulator antes de ejecutar MobSF. Lea [esto](dynamic_analyzer.md) antes de continuar.

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_ANALYZER_IDENTIFIER=<adb device identifier> opensecurity/mobile-security-framework-mobsf:latest
```

?> MobSF solo es compatible con Dynamic Analysis con Android **rooteado** versión 4.1 a 11.0 hasta API 30. La versión de Android 12 y superior no son compatibles.

Las opciones de Docker más comunes están disponibles en [MobSF Docker Options] (docker.md)