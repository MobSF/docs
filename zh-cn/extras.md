



# 附加需求

## REST API

MobSF提供了REST API。您可以从应用程序内访问最新的API文档。
***
## CI/CD

MobSF提供了REST API。您可以从应用程序内访问最新的API文档。

**MobSF CI/CD pipeline 集成**

* **MobSF - Bitrise** - https://www.netguru.com/codestories/ios-security-analysis-with-mobsf
* **MobSF - OWASP Glue** - https://medium.com/@omerlh/how-to-continuously-hacking-your-app-c8b32d1633ad
* **MobSF - Circle CI, OWASP Glue** - https://girlinjapan.net/running-mobsf-in-circleci-and-docker/
* **MobSF - Jenkins** - https://riis.com/blog/pentesting_at_scale/
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
* 在 `MobSF/settings.py`, 添加你的API Key `VT_API_KEY` 然后设置 `VT_ENABLED` 为 `True` 并重新启动 MobSF.
***
## AppMonsta Play商店信息

我们使用AppMonsta API从Google Play商店获取详细信息，这对我们的主要实现的安全措施。默认情况下禁用。要启用它，您需要AppMonsta API密钥。

* 从以下位置获取AppMonsta API密钥: [AppMonsta API Key](https://appmonsta.com/dashboard/get_api_key/)
* 在 `MobSF/settings.py`, 添加你的Api Key 到 `APPMONSTA_KEY` 然后重启 MobSF.
***
## 主目录支持

要向操作系统上的多个用户提供MobSF的个性化版本或将MobSF与渗透测试发行版捆绑在一起，您可能需要启用主目录支持。

要启用主目录支持，请转到 `MobSF/settings.py` 并将 `USE_HOME` 设置为 `True`。

这将确保

1. 现在，所有用户上传，数据库和下载均在用户主目录下的 `.MobSF` 目录中创建。
2. 用户配置从主目录中的`.MobSF/config.py`中读取。如果格式不正确或找不到文件，则从`MobSF/settings.py`本身读取用户配置。
***
## 使用Postgres DB代替SQLite

MobSF默认使用SQLite。如果需要，可以将后端更改为Postgres。

**安装psycopg2依赖项**

```bash
pip install psycopg2-binary
```

**修改配置n**

转到 `MobSF/settings.py`

注释以下内容

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': DB_DIR,
    }
}
```

现在取消注释以下内容

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

在Postgres中创建一个名为`mobsf`的数据库，并使用正确的用户名，密码和其他详细信息配置上述设置。

**应用迁移**

```bash
python manage.py makemigrations 
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
```

现在您可以重新启动MobSF服务器，并且已成功将Postgres配置为数据库。
