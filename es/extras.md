
# Funcionalidad Extra

## API REST

MobSF proporciona una API REST. Se puede acceder a la última versión de la documentación del API desde la aplicación.

***
## CI/CD

Se puede tomar ventaja del API de MobSF para CI/CD através de diferentes integraciónes.

**Integraciones para CI/CD de MobSF**

* **MobSF - Bitrise** - [iOS Security Analysis with MobSF](https://www.netguru.com/codestories/ios-security-analysis-with-mobsf) | [Run your security static analysis tests on the cloud with MobSF, AWS, and Bitrise](https://bitrise.io/blog/post/run-your-security-static-analysis-tests-on-the-cloud-with-mobsf-aws-and-bitrise)
* **MobSF - OWASP Glue** - [How To: (Continuously) Hacking Your App](https://medium.com/@omerlh/how-to-continuously-hacking-your-app-c8b32d1633ad)
* **MobSF - Jenkins** - [Pentesting at Scale](https://riis.com/blog/pentesting_at_scale/) |  [Achieving DevSecOps: Mobile App Security Integration Using Jenkins and MobSF](https://medium.com/@debasishkumardas5/achieving-devsecops-mobile-app-security-integration-using-jenkins-and-mobsf-187568f74d4c)
* **MobSF - Gitlab CI** [Running MobSF SAST using Gitlab CI Service](https://waristea.medium.com/running-mobsf-sast-using-gitlab-ci-service-7c3ac3a48648) | [GitLab CI template for MobSF](https://to-be-continuous.gitlab.io/doc/ref/mobsf/)
* **mobsfscan SAST CI/CD** - [mobsfscan](https://github.com/MobSF/mobsfscan)
***

## Análisis Estático de Masa

* Ejecutar el servidor de MobSF
`./run.sh` o `run.bat`
* Obtener la **llave del API** de la terminal.
* Ejecutar el archivo [mass_static_analysis.py](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/scripts/mass_static_analysis.py)

```bash
pip install requests
python mass_static_analysis.py
usage: mass_static_analysis.py [-h] [-d DIRECTORY] [-s IPPORT] [-k APIKEY]
                               [-r RESCAN]

optional arguments:
  -h, --help            show this help message and exit
  -d DIRECTORY, --directory DIRECTORY
                        Path to the directory that contains mobile app
                        binary/zipped source code
  -s IPPORT, --ipport IPPORT
                        IP address and Port number of a running MobSF Server.
                        (ex: 127.0.0.1:8000)
  -k APIKEY, --apikey APIKEY
                        MobSF REST API Key
  -r RESCAN, --rescan RESCAN
                        Run a fresh scan. Value can be 1 or 0 (Default: 0)
```

Ejemplo: 
```bash
python mass_static_analysis.py -s 127.0.0.1:8000  -k <llave_del_api> -d /home/files/
```
***
## VirusTotal Scan

VirusTotal Scan está desactivada por defecto. Se deberá de añadir la llave del API de VirusTotal antes de habilitarlo.

* Obtener la llave del API de VirusTotal [aquí](https://www.virustotal.com/#/join-us).
* Acceder a la API desde https://www.virustotal.com/en/user/[usuario]/apikey/.
* Dentro de `<directorio_home_del_usuario>/.MobSF/config.py` se debe de añadir la llave del API en `VT_API_KEY` y cambiar `VT_ENABLED` a `True`. Después de esto se debe de reiniciar MobSF.
***
## Información a través de AppMonsta para la Play Store

MobSF usa la API de AppMonsta para obtener los detalles de la Google Play Store como una precaución en dado caso de la que la implementación primaria llegara a fallar. Esta se encuentra desactivada por default; para activarla se necesitará la llave del API de AppMonsta.

* Obtener la llave del API de [AppMonsta](https://appmonsta.com/dashboard/get_api_key/)
* Dentro de `<directorio_home_del_usuario>/.MobSF/config.py` se deberá de añadir la llave del API a `APPMONSTA_KEY` y reiniciar la aplicación.
***
## Usar PostgreSQL en lugar de SQLite

De forma predeterminada, MobSF usa SQLite como base de datos. Sin embargo, puede cambiar a un backend de PostgreSQL si es necesario.

Para configurar PostgreSQL, configure las siguientes variables de entorno antes de iniciar MobSF:

    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=password
    POSTGRES_DB=mobsf
    POSTGRES_HOST=postgres
    POSTGRES_PORT=5432

**Aplicar migraciones**

```bash
poetry run python manage.py makemigrations 
poetry run python manage.py makemigrations StaticAnalyzer
poetry run python manage.py migrate
poetry run python manage.py create_roles
```

Ahora puede reiniciar el servidor MobSF y PostgreSQL se configurará correctamente como base de datos.