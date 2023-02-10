# Importar url de la apps dentro del proyecto

#### ***1. En nombreproyecto/urls.py, se agregan las rutas de los modelos de usuario/grupos por defecto y las rutas de las aplicaciones registradas***

    from django.contrib import admin
    from django.urls import path, include

    urlpatterns = [
        path('admin/', admin.site.urls), #rutas por defecto de admin se encontraran en 127.0.0.1:8000/admin/
        path('api/',include(('api.urls','api'))), #todas las rutas de la app "api" se encontraran en 127.0.0.1:8000/api/
    ]

#### ***2. si miramos la raiz http://127.0.0.1:8000/ saldrá asi:***

    Using the URLconf defined in tutorialapi.urls, Django tried these URL patterns, in this order:
    1. admin/
    2. api/
    The empty path didn’t match any of these.


En la app "api" se pueden crear las rutas asi (nombreproyecto/api/urls.py):
Se vuelven a colocar users y groups porque aquí van a estar en json y no en web como en admin

    from django.urls import path, include
    from .views import PersonaList,UserViewSet, GroupViewSet

    urlpatterns = [
        path('persona/',PersonaList.as_view(), name = 'persona_list'),
        path('users/',UserViewSet.as_view({'get': 'list'}), name = 'user_list'),
        path('groups/',GroupViewSet.as_view({'get': 'list'}), name = 'groups_list'),
    ]