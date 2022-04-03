heroku commands:
```sh
git clone REPOADRESS

py -m virtualenv -p python3 VENV
.\VENV\Scripts\activate
py -m pip install --upgrade pip
py -m pip install django
py -m pip install gunicorn
py -m pip install dj-database-url
py -m pip install whitenoise
py -m pip install psycopg2-binary
cd REPONAME

django-admin startproject PROJEKT
mv PROJEKT/*.* ./
mv PROJEKT/PROJEKT/* PROJEKT/
rmdir .\PROJEKT\PROJEKT\

py manage.py makemigrations
py manage.py migrate
py manage.py createsuperuser

django-admin startapp APP
mkdir APP/templates
mkdir APP/static
mkdir APP/static/css
mkdir APP/static/js
New-Item -Path 'APP/templates/index.html' -ItemType File
New-Item -Path 'APP/static/css/style.css' -ItemType File
New-Item -Path 'APP/static/js/script.js' -ItemType File

code .
```
register app and link static files

settings.py bottom:
```py
# ez a MIDDLEWARES közé:
'whitenoise.middleware.WhiteNoiseMiddleware',


# Heroku: Update database configuration from $DATABASE_URL.
import dj_database_url
db_from_env = dj_database_url.config(conn_max_age=500)
DATABASES['default'].update(db_from_env)

# INNEN szedegeti össze azokat a statikus fájlokat, amelyek nem tartoznak egyetlen apphoz sem:
STATICFILES_DIRS = [
    BASE_DIR/'static'
]

# IDE fogja collectelni a collectstatic
STATIC_ROOT = BASE_DIR / 'staticfiles'  

# itt a whitenoise alkalmazása
STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'

```
commands:
```sh
mkdir staticfiles
echo "bla" > staticfiles/nelegyenures.txt
echo "web: gunicorn PROJEKT.wsgi --log-file -" > Procfile
echo python-3.8.11 > runtime.txt
pip freeze > requirements.txt
code Procfile
code runtime.txt
code requirements.txt

heroku create HEROKUREMOTE
```
settings.py

```py
# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = False

ALLOWED_HOSTS = ['HEROKUREMOTE.herokuapp.com', '127.0.0.1']
```

```sh
git push heroku main
heroku run python manage.py migrate
heroku run python manage.py createsuperuser
heroku open
```















