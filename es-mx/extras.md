
# Funcionalidad Extra

## API REST

MobSF proporciona una API REST. Se puede acceder a la última versión de la documentación del API desde la aplicación.

***
## CI/CD

Se puede tomar ventaja del API de MobSF para CI/CD através de diferentes integraciónes.

**Integraciónes para CI/CD de MobSF**

* **MobSF - Bitrise** - https://www.netguru.com/codestories/ios-security-analysis-with-mobsf
* **MobSF - OWASP Glue** - https://medium.com/@omerlh/how-to-continuously-hacking-your-app-c8b32d1633ad
* **MobSF - Circle CI, OWASP Glue** - https://girlinjapan.net/running-mobsf-in-circleci-and-docker/
* **MobSF - Jenkins** - https://riis.com/blog/pentesting_at_scale/
* **MobSF - Github Actions** - https://github.com/marketplace/actions/github-action-for-mobsf
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

Por defecto, MobSF usa SQLite. Se puede cambiar el backend a PostgreSQL si se requiere.

**Instalar psycopg2**

```bash
pip install psycopg2-binary
```

**Modificar la Configuración**

Navegar a `mobsf/MobSF/settings.py` y comentar lo siguiente:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': DB_DIR,
    }
}
```

Enseguida se deberá de descomentar el siguiente bloque de código:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'mobsf',
        'USER': 'postgres',
        'PASSWORD': '',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

Después se deberá de crear una base de datos en PosgreSQL llamada `mobsf` y configurarla con las opciónes correctas que aparecen en el bloque de código anterior.

**Aplicar las Migraciónes**

```bash
python manage.py makemigrations 
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
```

Finalmente es necesario reiniciar el servidor de MobSF, después de ello se habrá configurado de manera éxitosa la nueva base de datos.