



# 追加情報

## REST API

MobSFはREST APIsを提供してイン佐生最新のAPIドキュメントにはアプリ内からアクセスできます。
***
## CI/CD

CI/CDでは、MobSF REST APIを利用できます。

**MobSF CI/CDパイプライン統合**

* **MobSF - Bitrise** - https://www.netguru.com/codestories/ios-security-analysis-with-mobsf
* **MobSF - OWASP Glue** - https://medium.com/@omerlh/how-to-continuously-hacking-your-app-c8b32d1633ad
* **MobSF - Circle CI, OWASP Glue** - https://girlinjapan.net/running-mobsf-in-circleci-and-docker/
* **MobSF - Jenkins** - https://riis.com/blog/pentesting_at_scale/
* **MobSF - Github Actions** - https://github.com/marketplace/actions/github-action-for-mobsf
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

MobSFはデフォルトではSQLiteを用いています。必要ならバックエンドをPostgresに変更できます。

**依存する psycopg2 のインストール**

```bash
pip install psycopg2-binary
```

**設定の変更**

`mobsf/MobSF/settings.py`を開く

以下をコメントアウト

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': DB_DIR,
    }
}
```

以下のコメントを解除

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

Postgres に名称`mobsf` のデータベースを作り、上の設定を正しいユーザー名、パスワード、その他詳細な情報に直します。

**マイグレーションの適用**

```bash
python manage.py makemigrations
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
```

これでMobSFサーバーを再起動することで、Postgresをデータベースとして正しく設定できました。
