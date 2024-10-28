



# Extra Features

## REST API

MobSF provides REST APIs. You can access the latest API docs from within the app.
***
## CI/CD

For CI/CD you can take advantage of MobSF REST API

**MobSF CI/CD pipeline integration**

* **MobSF - Bitrise** - [iOS Security Analysis with MobSF](https://www.netguru.com/codestories/ios-security-analysis-with-mobsf) | [Run your security static analysis tests on the cloud with MobSF, AWS, and Bitrise](https://bitrise.io/blog/post/run-your-security-static-analysis-tests-on-the-cloud-with-mobsf-aws-and-bitrise)
* **MobSF - OWASP Glue** - [How To: (Continuously) Hacking Your App](https://medium.com/@omerlh/how-to-continuously-hacking-your-app-c8b32d1633ad)
* **MobSF - Jenkins** - [Pentesting at Scale](https://riis.com/blog/pentesting_at_scale/) |  [Achieving DevSecOps: Mobile App Security Integration Using Jenkins and MobSF](https://medium.com/@debasishkumardas5/achieving-devsecops-mobile-app-security-integration-using-jenkins-and-mobsf-187568f74d4c)
* **MobSF - Gitlab CI** [Running MobSF SAST using Gitlab CI Service](https://waristea.medium.com/running-mobsf-sast-using-gitlab-ci-service-7c3ac3a48648) | [GitLab CI template for MobSF](https://to-be-continuous.gitlab.io/doc/ref/mobsf/)
* **mobsfscan SAST CI/CD** - [mobsfscan](https://github.com/MobSF/mobsfscan)
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
* In `<user_home_dir>/.MobSF/config.py`, add your API Key to `VT_API_KEY` and set `VT_ENABLED` to `True` and restart MobSF.
***
## AppMonsta Play Store Info

We use AppMonsta API to fetch details from Google Play Store as a fail safe to our primary implementation. It is disabled by default. To enable it, you need AppMonsta API Key.

* Get AppMonsta API Key from: [AppMonsta API Key](https://appmonsta.com/dashboard/get_api_key/)
* In `<user_home_dir>/.MobSF/config.py`, add your API Key to `APPMONSTA_KEY` and restart MobSF.
***
## Using Postgres DB instead of SQLite

By default, MobSF uses SQLite as its database. However, you can switch to a PostgreSQL backend if needed.

To configure PostgreSQL, set the following environment variables before starting MobSF:

    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=password
    POSTGRES_DB=mobsf
    POSTGRES_HOST=postgres
    POSTGRES_PORT=5432

**Apply Migrations**

```bash
poetry run python manage.py makemigrations 
poetry run python manage.py makemigrations StaticAnalyzer
poetry run python manage.py migrate
poetry run python manage.py create_roles
```

You can now restart the MobSF server, and PostgreSQL will be successfully configured as the database.
