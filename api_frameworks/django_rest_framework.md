# Django REST Framework (DRF) Cheat Sheet

## Installation

```bash
pip install djangorestframework
```

Add to `INSTALLED_APPS` in `settings.py`:

```python
INSTALLED_APPS = [
    ...
    'rest_framework',
]
```

## Basic Serializer

```python
from rest_framework import serializers

class UserSerializer(serializers.Serializer):
    id = serializers.IntegerField()
    name = serializers.CharField(max_length=100)
```

## ModelSerializer

```python
from rest_framework import serializers
from .models import User

class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ['id', 'name', 'email']
```

## Basic API View

```python
from rest_framework.views import APIView
from rest_framework.response import Response

class HelloView(APIView):
    def get(self, request):
        return Response({"message": "Hello, world!"})
```

## Function-Based View

```python
from rest_framework.decorators import api_view
from rest_framework.response import Response

@api_view(['GET'])
def hello(request):
    return Response({"message": "Hello"})
```

## ViewSet

```python
from rest_framework import viewsets
from .models import User
from .serializers import UserSerializer

class UserViewSet(viewsets.ModelViewSet):
    queryset = User.objects.all()
    serializer_class = UserSerializer
```

## Routers

```python
from rest_framework.routers import DefaultRouter
from .views import UserViewSet

router = DefaultRouter()
router.register(r'users', UserViewSet)
```

In `urls.py`:

```python
from django.urls import path, include

urlpatterns = [
    path('api/', include(router.urls)),
]
```

## Permissions

```python
from rest_framework.permissions import IsAuthenticated

class SecureView(APIView):
    permission_classes = [IsAuthenticated]

    def get(self, request):
        return Response({"secure": "data"})
```

## Authentication

Add to `settings.py`:

```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.TokenAuthentication',
    ]
}
```

Generate tokens:

```bash
python manage.py drf_create_token <username>
```

## Pagination

```python
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10
}
```

## Filtering, Searching, Ordering

Install and add:

```bash
pip install django-filter
```

```python
REST_FRAMEWORK = {
    'DEFAULT_FILTER_BACKENDS': [
        'django_filters.rest_framework.DjangoFilterBackend',
        'rest_framework.filters.SearchFilter',
        'rest_framework.filters.OrderingFilter',
    ]
}
```

In your view:

```python
class UserViewSet(viewsets.ModelViewSet):
    filterset_fields = ['name']
    search_fields = ['name', 'email']
    ordering_fields = ['id', 'name']
```

## Status Codes

```python
from rest_framework import status
from rest_framework.response import Response

return Response({"error": "not found"}, status=status.HTTP_404_NOT_FOUND)
```

## Exceptions

```python
from rest_framework.exceptions import NotFound

raise NotFound("User not found")
```

## Testing with APIClient

```python
from rest_framework.test import APIClient

client = APIClient()
response = client.get("/api/users/")
assert response.status_code == 200
```
