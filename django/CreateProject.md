# Crear proyecto django

#### ***1. Instalar Python 3***

<small><em>En la web oficial descargar el instalador si es windows</em></small> [python.org](https://www.python.org/downloads/)

Una vez instalado abrir consola de comandos preferida (cmd) y verificar version en windows con:

``py --version``

#### ***2. Crear environment***

Elegir la carpeta donde se creará el proyecto **(ejem: C:\laragon\www\proyectospython)**

``cd laragon\www\proyectospython``

Correr lo siguiente

``py -m venv .env``

**.env (puede ser cualquier nombre, luego debe considir abajo: nombrecarpeta\Scripts\activate)**

#### ***3. Activar envirioment***

``.env\Scripts\activate``

#### ***4. Instalar django***

Correr:

``pip install django``

Una vez terminada ver las versiones instaladas:

``pip freeze``

#### ***5. Crear proyecto django***

``django-admin startproject NombreProyectodjango``

Entrar a la carpeta del proyecto creado

``cd NombreProyectodjango``


#### ***6. Configuración hora e idioma, NombreProyectodjango/settings.py***

    LANGUAGE_CODE = 'es-es'

    TIME_ZONE = 'America/Santiago'

#### ***7. Correr el server***

``py manage.py migrate``

``py manage.py runserver``

Pegar en el navegador la ip de la consola (ejem: http://127.0.0.1:8000)
