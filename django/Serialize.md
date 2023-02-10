# Serializar modelos (response: json)

Una vez creado el proyecto: [Como crear proyecto django](https://github.com/orijmm/codigostest/blob/main/django/CreateProject.md) 

Agregado Django Rest Framewrok: [django rest](https://github.com/orijmm/codigostest/blob/main/django/DjangoApiRest.md) 

#### ***1. Crear archivo serializers.py, Nombreproyecto/api/serializers.py:***

    from django.contrib.auth.models import User, Group
    from rest_framework import serializers
    from .models import Persona

    class PersonaSerializer(serializers.ModelSerializer):
        class Meta:
            model = Persona
            fields = (
                'id',
                'nombre',
                'apellido',
            )
        
    class GroupSerializer(serializers.HyperlinkedModelSerializer):
        class Meta:
            model = Group
            fields = ['name','id']

    class UserSerializer(serializers.HyperlinkedModelSerializer):
        groups = GroupSerializer(many=True) #relacion uno a muchos
        class Meta:
            model = User
            fields = ['username', 'email', 'id', 'groups']

Aqui se agregar la version serializada al modelo creado persona y a los dos modelos que vienen por defecto en django user y group.

Para persona se usa serializers.ModelSerializer
Para user y groups se usa serializers.HyperlinkedModelSerializer

La diferencia es que HyperlinkedModelSerializer coloca en la relación user/groups el resto de la data de groups, como nombre e id, con ModelSerializer solo mostraría el id.


#### ***2. Modificar Nombreproyecto/api/views.py***

    from rest_framework import viewsets
    from rest_framework import permissions
    from .models import Persona
    from .serializers import PersonaSerializer, UserSerializer, GroupSerializer

    class PersonaList(generics.ListCreateAPIView):
        queryset = Persona.objects.all()
        serializer_class = PersonaSerializer

    class UserViewSet(viewsets.ModelViewSet):
        """
        API endpoint that allows users to be viewed or edited.
        """
        queryset = User.objects.all().order_by('-date_joined')
        serializer_class = UserSerializer
        # permission_classes = [permissions.IsAuthenticated]


    class GroupViewSet(viewsets.ModelViewSet):
        """
        API endpoint that allows groups to be viewed or edited.
        """
        queryset = Group.objects.all()
        serializer_class = GroupSerializer

Aqui se llaman los modelos serializados en serializers.py y se hace la consulta en queryset

#### ***3. para probarlo colocar en urls.py***

    from .views import PersonaList,UserViewSet, GroupViewSet

    urlpatterns = [
        path('persona',PersonaList.as_view(), name = 'persona_list'),
        path('users',UserViewSet.as_view({'get': 'list'}), name = 'user_list'),
        path('groups',GroupViewSet.as_view({'get': 'list'}), name = 'groups_list'),
    ]

los que son HyperlinkedModelSerializer se coloca: {'get': 'list'} en as_view()

#### ***4. Revisar***

Conectar las rutas entre apps: [Urls entre apps](https://github.com/orijmm/codigostest/blob/main/django/ConnectURLBeetweenApps.md) 

Para el correcto ruteo y link en postman