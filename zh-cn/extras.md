



# 附加需求

## REST API

MobSF提供了REST API。您可以从应用程序内访问最新的API文档。
***
## CI/CD

MobSF提供了REST API。您可以从应用程序内访问最新的API文档。

**MobSF CI/CD pipeline 集成**

* **MobSF - Bitrise** - [iOS Security Analysis with MobSF](https://www.netguru.com/codestories/ios-security-analysis-with-mobsf) | [Run your security static analysis tests on the cloud with MobSF, AWS, and Bitrise](https://bitrise.io/blog/post/run-your-security-static-analysis-tests-on-the-cloud-with-mobsf-aws-and-bitrise)
* **MobSF - OWASP Glue** - [How To: (Continuously) Hacking Your App](https://medium.com/@omerlh/how-to-continuously-hacking-your-app-c8b32d1633ad)
* **MobSF - Jenkins** - [Pentesting at Scale](https://riis.com/blog/pentesting_at_scale/) |  [Achieving DevSecOps: Mobile App Security Integration Using Jenkins and MobSF](https://medium.com/@debasishkumardas5/achieving-devsecops-mobile-app-security-integration-using-jenkins-and-mobsf-187568f74d4c)
* **MobSF - Gitlab CI** [Running MobSF SAST using Gitlab CI Service](https://waristea.medium.com/running-mobsf-sast-using-gitlab-ci-service-7c3ac3a48648) | [GitLab CI template for MobSF](https://to-be-continuous.gitlab.io/doc/ref/mobsf/)
* **mobsfscan SAST CI/CD** - [mobsfscan](https://github.com/MobSF/mobsfscan)
***
## 质量静态分析

* 运行MobSF服务器.
`./run.sh` or `run.bat`
* 从控制台获取**REST API密钥**。
* 运行 [mass_static_analysis.py](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/scripts/mass_static_analysis.py)

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

示例: 
```bash
python mass_static_analysis.py -s 127.0.0.1:8000  -k <rest_api_key> -d /home/files/
```
***
## VirusTotal Scan

默认情况下，VirusTotal Scan是禁用的。您需要先添加VirusTotal API密钥，然后才能启用它。

* 在此处获取VirusTotal API密钥 [here](https://www.virustotal.com/#/join-us)
* 从 `https://www.virustotal.com/en/user/[用户名]/apikey/` 访问您的API密钥
* 在 `<user_home_dir>/.MobSF/config.py`, 添加你的API Key `VT_API_KEY` 然后设置 `VT_ENABLED` 为 `True` 并重新启动 MobSF.
***
## AppMonsta Play商店信息

我们使用AppMonsta API从Google Play商店获取详细信息，这对我们的主要实现的安全措施。默认情况下禁用。要启用它，您需要AppMonsta API密钥。

* 从以下位置获取AppMonsta API密钥: [AppMonsta API Key](https://appmonsta.com/dashboard/get_api_key/)
* 在 `<user_home_dir>/.MobSF/config.py`, 添加你的Api Key 到 `APPMONSTA_KEY` 然后重启 MobSF.
***
## 使用Postgres DB代替SQLite

默认情况下，MobSF 使用 SQLite 作为其数据库。但是，如果需要，您可以切换到 PostgreSQL 后端。

要配置 PostgreSQL，请在启动 MobSF 之前设置以下环境变量：

    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=password
    POSTGRES_DB=mobsf
    POSTGRES_HOST=postgres
    POSTGRES_PORT=5432

**应用迁移**

````bash
poetry run python manage.py makemigrations 
poetry run python manage.py makemigrations StaticAnalyzer
poetry run python manage.py migrate
poetry run python manage.py create_roles
````

您现在可以重新启动 MobSF 服务器，并且 PostgreSQL 将成功配置为数据库。