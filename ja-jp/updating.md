# MobSFの更新

MobSFを更新する場合、ほとんどの場合、データベースの移行を実行する必要があります。そうしないと、次のようなエラーが表示されます。
```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named
```

## Linux/Mac

```bash
cd Mobile-Security-Framework-MobSF/
git pull origin master
. venv/bin/activate
pip install --no-cache-dir --use-deprecated=legacy-resolver -r requirements.txt
python manage.py makemigrations
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
deactivate
```

## Windows

```batch
cd Mobile-Security-Framework-MobSF/
git pull origin master
.\venv\Scripts\activate
pip install --no-cache-dir --use-deprecated=legacy-resolver -r requirements.txt
python manage.py makemigrations
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
deactivate
```

!>上記でうまくいかない場合は、`~/.MobSF` または `C:\Users\<user>\.MobSF` を削除して、`setup.sh` または `setup.bat` を再度実行する必要があるかもしれませんが、これは以前のスキャン結果を削除します。
