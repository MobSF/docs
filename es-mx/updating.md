# Actualizando MobSF

En la mayor parte de los casos, si se está actualizando MobSF, se deberá de realizar una migración de la base de datos; de lo contrario se podrían presentar errores como el siguiente:

```
[ERROR] Saving to DB (E:\Mobile-Security-Framework-MobSF\StaticAnalyzer\views\android\db_interaction.py,
 LINE 236 "static_db.save()"): table StaticAnalyzer_staticanalyzerandroid has no column named 
```

## Linux/MacOS

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

!> Si los cambios anteriores no funcionaron, se debe de ejecutar el script `setup.sh` o `setup.bat` de nuevo; esto borrará los resultados de los escaneos previos.
