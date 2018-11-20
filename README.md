# django-python-cheetsheet


### **Virtual Environmnents**

- Installing virtualenv with pip

``` bash
pip3 install virtualenv
```

note only have to do once ^

- Inside a project you just created 

```bash
virtualenv .env -p python3
source .env/bin/activate
```

- Setup ```.gitignore```

```
touch .gitignore
```

- add ```.env``` inside the .gitignore, now you initalize git and make your first commit.  

### Installing modules from a cloned Repo

- Start an environment 
- ```pip3 install -r requirements.txt```



### Adding Modules in your environment and Creating Requirements.txt

```pip3 freeze > requirements.txt```

### **Django admin commands**

- To start a project 
```
django-admin startproject project_name
```

- To start an app, (which are inside of django projects 
```
django-admin startapp tunr
```

- Adding the app to your project 

```settings.py in djangoProject
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'appname'
]
```


- Installing modules (do this where ```requirements.txt``` is)
```
pip3 install django
pip3 install psycopg2
```

- Add installed modules to ```requirements.txt```

```
pip3 freeze > requirements.txt
```
### Running Server
```python3 manage.py runserver```



### **Setting up psql**
```
$ psql
> CREATE DATABASE databasename;
> CREATE USER whateveryourusernameis WITH PASSWORD 'passwordasastring';
GRANT ALL PRIVILEGES ON DATABASE databasename TO whateveryourusernameis;
> \q
```

- Inside of django 

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'databasename',
        'USER': 'whateveryourusernameis',
        'PASSWORD': 'passwordasastring',
        'HOST': 'localhost'
    }
}
```

- Note here ```HOST``` is wherever your DB is hosted, so if you're deploying you have to change that to where your DB is hosted

- Also the engine is whatever module you are using to connect to your database in this case I'm using ```psycopg2```


### Useful Modules 

[django-cors-headers](https://github.com/ottoyiu/django-cors-headers)


### Setting up relations
- Note its easier to setup user models at the beginning then adding it later, so think up your models before you start coding!

```
from django.db import models
from django.contrib.auth.models import User

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=100)
    year = models.IntegerField(default = 0)
    created_by = models.ForeignKey(User, on_delete=models.CASCADE, related_name='books')

    def __str__(self):
        return self.title
```


### Migrations and Migrate

```
python3 mangage.py makemigrations ## Creates tables 
python3 mangape.py migrate ## commits migration to database
```

Docs - [Relations](https://docs.djangoproject.com/en/2.1/topics/db/examples/)

### Auth 

```
from django.contrib import auth
```

- useful commands 

```
auth.logout(request)
auth.login(request, user_object)
auth.authenticate(username=data["username"], password=data["password"])
```



