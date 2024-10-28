



# 追加情報

## REST API

MobSFはREST APIsを提供してイン佐生最新のAPIドキュメントにはアプリ内からアクセスできます。
***
## CI/CD

CI/CDでは、MobSF REST APIを利用できます。

**MobSF CI/CDパイプライン統合**

* **MobSF - Bitrise** - [iOS Security Analysis with MobSF](https://www.netguru.com/codestories/ios-security-analysis-with-mobsf) | [Run your security static analysis tests on the cloud with MobSF, AWS, and Bitrise](https://bitrise.io/blog/post/run-your-security-static-analysis-tests-on-the-cloud-with-mobsf-aws-and-bitrise)
* **MobSF - OWASP Glue** - [How To: (Continuously) Hacking Your App](https://medium.com/@omerlh/how-to-continuously-hacking-your-app-c8b32d1633ad)
* **MobSF - Jenkins** - [Pentesting at Scale](https://riis.com/blog/pentesting_at_scale/) |  [Achieving DevSecOps: Mobile App Security Integration Using Jenkins and MobSF](https://medium.com/@debasishkumardas5/achieving-devsecops-mobile-app-security-integration-using-jenkins-and-mobsf-187568f74d4c)
* **MobSF - Gitlab CI** [Running MobSF SAST using Gitlab CI Service](https://waristea.medium.com/running-mobsf-sast-using-gitlab-ci-service-7c3ac3a48648) | [GitLab CI template for MobSF](https://to-be-continuous.gitlab.io/doc/ref/mobsf/)
* **mobsfscan SAST CI/CD** - [mobsfscan](https://github.com/MobSF/mobsfscan)
***
## 多量の静的解析を一度に実施

* MobSFサーバーを起動します。
   `./run.sh` または `run.bat`
* コンソールから**REST APIキー**を取得します。
* [mass_static_analysis.py](https://github.com/MobSF/Mobile-Security-Framework-MobSF/blob/master/scripts/mass_static_analysis.py) を実行します。

```bash
pip install requests
python mass_static_analysis.py
usage: mass_static_analysis.py [-h] [-d DIRECTORY] [-s IPPORT] [-k APIKEY]
                               [-r RESCAN]

オプション引数:
  -h, --help            このヘルプメッセージを表示して終了します。
  -d DIRECTORY, --directory DIRECTORY
                        モバイルアプリまたはZIPされたソースコードを格納した
                        ディレクトリへのパス
  -s IPPORT, --ipport IPPORT
                        MobSFサーバーが実行されているIPアドレスとポート番号
                        (例: 127.0.0.1:8000)
  -k APIKEY, --apikey APIKEY
                        MobSF REST APIキー
  -r RESCAN, --rescan RESCAN
                        過去の結果を破棄した再スキャンを実行する。値は1 または 0を指定 (デフォルト: 0)
```

例:
```bash
python mass_static_analysis.py -s 127.0.0.1:8000  -k <rest_api_key> -d /home/files/
```
***
## VirusTotalスキャン

VirusTotalはデフォルトでは無効化されています有効化する前に、VirusTotal API Keyを追加する必要があります。

* VirusTotal API Key を [こちら](https://www.virustotal.com/#/join-us) で得てください
* API Keyは https://www.virustotal.com/en/user/[username]/apikey/ からアクセスできます。
* `<user_home_dir>/.MobSF/config.py`に、API Key を`VT_API_KEY` に設定し、`VT_ENABLED` を `True` に設定した上で MobSF を再起動してください。
***
## AppMonsta Play Store情報

MobSFではもともとの実装のフェイルセーフとして、AppMonsta APIを用いてGoogle Play Storeから詳細な情報を取得しています。デフォルトでは無効化されています。有効化するには、AppMonsta API Keyが必要です。

* AppMonsta API Key を [AppMonsta API Key](https://appmonsta.com/dashboard/get_api_key/) で得てください
* `<user_home_dir>/.MobSF/config.py`に、API Key を`APPMONSTA_KEY` に設定して、MobSF を再起動してください。
***
## SQLiteの代わりにPostgres DBを用いる

デフォルトでは、MobSF はデータベースとして SQLite を使用します。ただし、必要に応じて PostgreSQL バックエンドに切り替えることができます。

PostgreSQL を構成するには、MobSF を開始する前に次の環境変数を設定します。

    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=password
    POSTGRES_DB=mobsf
    POSTGRES_HOST=postgres
    POSTGRES_PORT=5432

**移行の適用**

```bash
poetry run python manage.py makemigrations 
poetry run python manage.py makemigrations StaticAnalyzer
poetry run python manage.py migrate
poetry run python manage.py create_roles
```

これで MobSF サーバーを再起動できるようになり、PostgreSQL がデータベースとして正常に構成されます。