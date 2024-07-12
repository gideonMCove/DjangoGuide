# DjangoGuide

mkdir {database}_project
cd {database}_project

```sh
sudo apt install python3-pip
```
```sh
pip install pipenv --user
```

```sh
cat << EOF >> ~/.zshrc

export PATH="$(python3 -m site --user-base)/bin:\$PATH"
EOF
```

***close terminal/open terminal***

To confirm download:

```sh
pipenv --version 
```
This will take a while :

```sh
pipenv install django 
```

```sh
pipenv install psycopg2-binary  
```
```sh
pipenv run django-admin startproject {database}_django .
```
```sh
pipenv shell
```
```sh
 django-admin startapp {database}
```
 In {database}_django/settings.py find the INSTALLED_APPS constant dictionary. On the bottom line of the INSTALLED_APPS list, add '{database}'. 

this should be in the root file of the project:
```sh
 touch settings.sql
```


 inside settings.sql,
 ```sh
    CREATE DATABASE {database};
    CREATE USER {user} WITH PASSWORD '{password}';
    GRANT ALL PRIVILEGES ON DATABASE {database} TO {user};
```
```sh
 psql -f settings.sql
```

    IF you are getting an error about a postgres user being needed, enter this:
        psql -U postgres -f settings.sql

In {database}_django/settings.py, find the DATABASES constant dictionary. Let's edit it to look like this:
 ```sh
    DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': '{database}',
        'USER': '{user}',
        'PASSWORD': '{password}',
        'HOST': 'localhost'
    }
}
```
```sh
pipenv shell
```
```sh
cd {database}_project
```
```sh
python3 manage.py runserver
```
# Models 

### Example: 
(in /{database}_project/{database}/models.py)
class Artist(models.Model):
    name = models.CharField(max_length=100)
    nationality = models.CharField(max_length=100)
    photo_url = models.TextField()
```sh    
 python3 manage.py makemigrations
```
```sh
 python3 manage.py migrate
```
To create admin priviledges for your DB:
```sh
 python3 manage.py createsuperuser
```

