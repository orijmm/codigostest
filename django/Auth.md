# Agregar auth token

Una vez creado el proyecto: [Como crear proyecto django](https://github.com/orijmm/codigostest/blob/main/django/CreateProject.md) 

Agregado Django Rest Framewrok: [django rest](https://github.com/orijmm/codigostest/blob/main/django/DjangoApiRest.md) 

Serializado los modelos: [Serializar modelos](https://github.com/orijmm/codigostest/blob/main/django/Serialize.md) 

Conectar las rutas entre apps: [Urls entre apps](https://github.com/orijmm/codigostest/blob/main/django/ConnectURLBeetweenApps.md) 


#### ***1. Agregar en settings.py***

     INSTALLED_APPS = [
      ...
      'rest_framework.authtoken'
    ]

    REST_FRAMEWORK = {
        'DEFAULT_PERMISSION_CLASSES': [
            'rest_framework.permissions.IsAuthenticated',
        ],
        'DEFAULT_AUTHENTICATION_CLASSES': (
            'rest_framework.authentication.TokenAuthentication',
        ),
    }

#### ***2. en api/urls.py***

    from rest_framework.authtoken import views
    ...
    urlpatterns = [
     path('api_generate_token', views.obtain_auth_token),
    ]

#### ***3. Correr migraciones***

``py manage.py migrate``

#### ***4. Probar postman:***

``http://127.0.0.1:8000/api/api_generate_token``

body:

    {
        "username": "admin",
        "password": "12345678"
    }

Deberia responder:

    {
    "token": "8246d65769eaa7d603af510658d3038ef57bcf8f"
    }

#### ***5. Mirar links con token:***

se manda en el Headers

Authorization: Token 8246d65769eaa7d603af510658d3038ef57bcf8f