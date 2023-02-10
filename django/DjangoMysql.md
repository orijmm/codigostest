# Cambiar base de datos a mysql

Una vez creado el proyecto: [Como crear proyecto django](https://github.com/orijmm/codigostest/blob/main/django/CreateProject.md) 

#### ***1. Cambiar base de datos sqlite3 a mysql***

Intalar la libreria para mysql

``pip install pymysql``

En ***NombreProyecto/NombreProyecto/__init__.py*** colocar:

    import pymysql
    pymysql.install_as_MySQLdb()

En ***NombreProyecto/NombreProyecto/settings.py***

Cambiar esto:

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }

Por esto:

    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'djangotest',
            'USER': 'root',
            'PASSWORD': '',
            'HOST': '127.0.0.1',
            'PORT': '3306',
        }
    }

Volver a migrar:

``py manage.py migrate``
