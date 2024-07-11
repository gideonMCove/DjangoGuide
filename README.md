# DjangoGuide

mkdir {database}_project
cd {database}_project

sudo apt install python3-pip

pip install pipenv --user

cat << EOF >> ~/.zshrc

export PATH="$(python3 -m site --user-base)/bin:\$PATH"
EOF

close terminal/open terminal

pipenv --version / to confirm download

pipenv install django / this takes a while

pipenv install psycopg2-binary / this takes a while

pipenv run django-admin startproject tunr_django .

pipenv shell

 django-admin startapp tunr

 In tunr_django/settings.py find the INSTALLED_APPS constant dictionary. On the bottom line of the INSTALLED_APPS list, add tunr. 

 touch settings.sql

 inside settings.sql,    
    CREATE DATABASE {database};
    CREATE USER {user} WITH PASSWORD '{password}';
    GRANT ALL PRIVILEGES ON DATABASE {database} TO {user};

 psql -f settings.sql
    IF you are getting an error about a postgres user being needed, enter this:
        psql -U postgres -f settings.sql

In tunr_django/settings.py, find the DATABASES constant dictionary. Let's edit it to look like this:
    DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': '{database}',
        'USER': '{user}',
        'PASSWORD': '{password}',
        'HOST': 'localhost'
    }
}



