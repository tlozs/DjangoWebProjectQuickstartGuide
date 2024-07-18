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
py -m pip install psycopg2-binary

cd REPONAME
```

# 5. Start project with static files
```sh
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
mkdir APP/static/images
New-Item -Path 'APP/templates/index.html' -ItemType File
New-Item -Path 'APP/static/css/style.css' -ItemType File
New-Item -Path 'APP/static/js/script.js' -ItemType File
code .
code PROJEKT/settings.py
code PROJEKT/urls.py
code APP/views.py
code APP/templates/index.html

```

# 6. Register APP in ``settings.py``, ``urls.py``, ``views.py`` respectively
```py
INSTALLED_APPS = [
    'APP',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
```py
from APP.views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', index),
]
```
```py
def index(request):
    template='index.html'
    context={}
    return render(request, template, context)
```

# 7. link static files
```html
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" type="text/css" href="{% static 'css/style.css' %}">
    <script src="{% static 'js/script.js' %}"></script>
    <title>Title</title>
</head>
<body>
    
</body>
</html>
```

# 8. Update ``settings.py`` allowed hosts
```py
ALLOWED_HOSTS = ['127.0.0.1', 'localhost']
```



























