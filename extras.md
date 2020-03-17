



# Extra Features

## REST API

MobSF provides REST APIs. You can access the latest API docs from within the app.
***
## CI/CD

For CI/CD you can take advantage of MobSF REST API

**MobSF CI/CD pipeline integration**

* **MobSF - Bitrise** - https://www.netguru.com/codestories/ios-security-analysis-with-mobsf
* **MobSF - OWASP Glue** - https://medium.com/@omerlh/how-to-continuously-hacking-your-app-c8b32d1633ad
* **MobSF - Circle CI, OWASP Glue** - https://girlinjapan.net/running-mobsf-in-circleci-and-docker/
* **MobSF - Jenkins** - https://riis.com/blog/pentesting_at_scale/
***
## Mass Static Analysis

* Run MobSF server.
`./run.sh` or `run.bat`
* Obtain the **REST API key** from console.
* Run [mass_static_analysis.py](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/scripts/mass_static_analysis.py)

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

Example: 
```bash
python mass_static_analysis.py -s 127.0.0.1:8000  -k <rest_api_key> -d /home/files/
```
***
## VirusTotal Scan

VirusTotal Scan is disabled by default. You need to add your VirusTotal API Key before enabling it.

* Get VirusTotal API Key [here](https://www.virustotal.com/#/join-us)
* Access your API Key from https://www.virustotal.com/en/user/[username]/apikey/.
* In `MobSF/settings.py`, add your API Key to `VT_API_KEY` and set `VT_ENABLED` to `True` and restart MobSF.
***
## AppMonsta Play Store Info

We use AppMonsta API to fetch details from Google Play Store as a fail safe to our primary implementation. It is disabled by default. To enable it, you need AppMonsta API Key.

* Get AppMonsta API Key from: [AppMonsta API Key](https://appmonsta.com/dashboard/get_api_key/)
* In `MobSF/settings.py`, add your API Key to `APPMONSTA_KEY` and restart MobSF.
***
## Home Directory Support

To provide personalized version of MobSF to multiple users on an OS or to bundle MobSF with a pentesting distro you might need the home directory support enabled.

To enable Home Directory support, go to `MobSF/settings.py` and set `USE_HOME` to `True`

This will ensure

1. All the user uploads, database, and downloads are now created in `.MobSF` directory under user's home directory.
2. User configurations are read from `.MobSF/config.py` in home directory. If the format is incorrect or the file is not found, user configurations are read from `MobSF/settings.py` itself.
***
## Using Postgres DB instead of SQLite

MobSF by default uses SQLite. You can change the backend to Postgres if required.

**Install psycopg2 dependency**

```bash
pip install psycopg2-binary
```

**Modify Configuration**

Go to `MobSF/settings.py`

Comment the following

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': DB_DIR,
    }
}
```

Now uncomment the following

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

Create a database in Postgres named `mobsf` and configure the above settings with correct username, password and other details.

**Apply Migrations**

```bash
python manage.py makemigrations 
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
```

Now you can restart MobSF server and you have successfully configured Postgres as your database.
