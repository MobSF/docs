# Updating MobSF

If you are updating MobSF, In most cases you might have to perform database migrations or you will see errors such as
```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named 
```

## Linux/Mac

```bash
cd Mobile-Security-Framework-MobSF/
git pull origin master
. venv/bin/activate
pip install -r requirements.txt
python manage.py makemigrations
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
deactivate
```

## Windows

```bash
cd Mobile-Security-Framework-MobSF/
git pull origin master
.\venv\Scripts\activate
pip install -r requirements.txt
python manage.py makemigrations
python manage.py makemigrations StaticAnalyzer
python manage.py migrate
deactivate
```

!>If the above changes didn't work, you might have to run `setup.sh` or `setup.bat` again which will delete your previous scan results.
