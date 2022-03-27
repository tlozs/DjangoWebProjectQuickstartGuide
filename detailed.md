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
virtualenv -p python3 VENV
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

2. navigate to the folder in which ``manage.py`` is located
```sh
cd PROJEKT
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

3. you may need to repeat step 4 to migrate database changes again

# 6. Create and register an application called ``APP``

1. create it using this command
```sh
django-admin startapp APP
```

2. register it in ``settings.py``
```py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'APP',
]
```

3. create a ``templates`` folder for your application
```sh
  mkdir APP/templates
```

4. insert an ``index.html`` into the templates folder
```sh
New-Item -Path 'APP/templates/index.html' - ItemType File
```

5. create a view for the template in ``APP/views.py``
```py
def index(request):
    template='index.html'
    context={}
    return render(request, template, context)
```

6. register a template url in ``urls.py``
```py
# you need to import the view
from APP.views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    
    # and define a url for it
    path('', index),
]
```

















