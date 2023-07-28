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

Ahora puede acceder a la interfaz web de MobSF en `http://127.0.0.1:8000` en su navegador web.

### Ejecute MobSF con soporte de análisis estático y dinámico

También puede ejecutar MobSF con soporte de análisis estático y dinámico utilizando la imagen acoplable de MobSF v3.6.9 en adelante.

!> Debe ejecutar cualquiera de los **[compatibles](dynamic_analyzer.md)** Genymotion Android VM/Android Studio Emulator antes de ejecutar MobSF. Lea [esto](dynamic_analyzer.md) antes de continuar.

```
docker run -it --rm -p 8000:8000 -p 1337:1337 -e MOBSF_ANALYZER_IDENTIFIER=<adb device identifier> opensecurity/mobile-security-framework-mobsf:latest
```

?> MobSF solo es compatible con Dynamic Analysis con Android **rooteado** versión 4.1 a 11.0 hasta API 30. La versión de Android 12 y superior no son compatibles.

Las opciones de Docker más comunes están disponibles en [MobSF Docker Options] (docker.md)

## Cómo usar MobSF

Este video de Defcon Demo Labs 2020 explica algunas de las funciones básicas de MobSF.

<iframe width="760" height="515" src="https://www.youtube.com/embed/1NIQs82n3nw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### Otros recursos

* [Presentaciones y diapositivas de MobSF anteriores](https://mobsf.github.io/Mobile-Security-Framework-MobSF/presentations.html)
* [Curso de aprendizaje electrónico: Evaluación automatizada de seguridad de aplicaciones móviles con MobSF -MAS](https://opsecx.com/index.php/product/automated-mobile-application-security-assessment-with-mobsf/)
