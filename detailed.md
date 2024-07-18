# DjangoWebProjectQuickstartGuide
Detailed guide on how to start a Django web project using git(hub) and python.

You may need to edit the ``ExecutionPolicy`` to be able to run some commands:
```sh
Set-ExecutionPolicy Unrestricted -Scope Process
```

# 0. Installing VENV and Django

```sh
py -m pip install --user --upgrade pip
py -m pip install --user virtualenv
py -m pip install --user -U Django
```

# 1. Creating and cloning GitHub remote repo

1. create a repo on **github.com**
2. add python **.gitignore** template
3. clone the created repo to the local machine:
```sh
git clone REPOADRESS
```

# 2. Initializing VENV

1. create a virtual enviroment with name ``VENV`` next to the repo, not inside the repo
```sh
py -m virtualenv -p python3 VENV
```

2. activate VENV
```sh
.\VENV\Scripts\activate
```

3. install the requirements
```sh
py -m pip install --upgrade pip
py -m pip install django
py -m pip install gunicorn
py -m pip install dj-database-url
py -m pip install whitenoise
py -m pip install django-rest-framework
py -m pip install psycopg2-binary
```

4. see what's inside
```sh
pip freeze
```

5. navigate inside the repo
```sh
cd REPONAME
```

# 3. Start a project and see it working

1. start a Django project with name ``PROJEKT`` inside the repo
```sh
django-admin startproject PROJEKT
```

2. reorganize file hierarchy
```sh
mv PROJEKT/*.* ./
mv PROJEKT/PROJEKT/* PROJEKT/
rmdir .\PROJEKT\PROJEKT\
```

3. run the server and see if it's working on ``127.0.0.1:8000`` or ``localhost:8000`` (they are the same)
```sh
py manage.py runserver
``` 

# 4. create local database

1. prepare changes for migration
```sh
py manage.py makemigrations
```

2. migrate changes
```sh
py manage.py migrate
```

# 5. Create an admin profile

1. run this to create the profile
```sh
py manage.py createsuperuser
```

2. the admin site is found on ``127.0.0.1:8000/admin`` or ``localhost:8000/admin`` by default

3. you may need to repeat **step 4** to migrate database changes again

# 6. Create and register an application called ``APP`` with basic static files

1. create it using this command
```sh
django-admin startapp APP
```

2. create a ``templates`` folder for your application
```sh
mkdir APP/templates
```

3. create ``static`` folders
```sh
mkdir APP/static
mkdir APP/static/css
mkdir APP/static/js
mkdir APP/static/images
```

4. insert an ``index.html`` into the ``templates`` folder and static files into the ``static`` folder
```sh
New-Item -Path 'APP/templates/index.html' -ItemType File
New-Item -Path 'APP/static/css/style.css' -ItemType File
New-Item -Path 'APP/static/js/script.js' -ItemType File
```

5. open files with VSCode
```sh
code .
code PROJEKT/settings.py
code PROJEKT/urls.py
code APP/views.py
code APP/templates/index.html
```

6. register the APP in ``settings.py`` (the order of apps is important)
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

7. create a view for the template in ``APP/views.py``
```py
def index(request):
    template='index.html'
    context={}
    return render(request, template, context)
```

8. register a template url in ``urls.py``
```py
# you need to import the view
from APP.views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    
    # and define a url for it
    path('', index),
]
```

9. link the static files to your template in ``index.html``
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

# 7. edit ``settings.py`` to allow localhost to host your development server
```py
ALLOWED_HOSTS = ['127.0.0.1', 'localhost']
```




