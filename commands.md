# 1. Execution Policy
```sh
Set-ExecutionPolicy Unrestricted -Scope Process
```

# 2. Install or update
```sh
py -m pip install --user --upgrade pip
py -m pip install --user virtualenv
py -m pip install --user -U Django
```

# 3. Clone
```sh
git clone REPOADRESS
```

# 4. VENV
```sh
py -m virtualenv -p python3 VENV
.\VENV\Scripts\activate
py -m pip install --upgrade pip
py -m pip install django
py -m pip install gunicorn
py -m pip install dj-database-url
py -m pip install whitenoise
py -m pip install django-rest-framework
cd REPONAME
```

# 5. Start project
```sh
django-admin startproject PROJEKT
cd PROJEKT
py manage.py makemigrations
py manage.py migrate
py manage.py createsuperuser
django-admin startapp APP
mkdir APP/templates
New-Item -Path 'APP/templates/index.html' -ItemType File
```

# 6. Register APP in ``settings.py``, ``urls.py``, ``views.py``
