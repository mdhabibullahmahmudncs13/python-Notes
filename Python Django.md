# Python Django

Django is a high-level Python web framework for rapid development.

## Installation

```bash
pip install django
```

## Create Project

```bash
django-admin startproject myproject
cd myproject
```

## Project Structure

```
myproject/
    manage.py
    myproject/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

## Create App

```bash
python manage.py startapp myapp
```

## Run Server

```bash
python manage.py runserver

# Access at http://127.0.0.1:8000/
```

## Models

Define database schema:

```python
# myapp/models.py
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=100)
    published_date = models.DateField()
    price = models.DecimalField(max_digits=6, decimal_places=2)
    
    def __str__(self):
        return self.title
```

## Migrations

```bash
# Create migrations
python manage.py makemigrations

# Apply migrations
python manage.py migrate
```

## Views

Handle requests:

```python
# myapp/views.py
from django.http import HttpResponse
from django.shortcuts import render
from .models import Book

def index(request):
    return HttpResponse("Hello, Django!")

def book_list(request):
    books = Book.objects.all()
    return render(request, 'books.html', {'books': books})

def book_detail(request, id):
    book = Book.objects.get(id=id)
    return render(request, 'book_detail.html', {'book': book})
```

## URLs

Route requests:

```python
# myapp/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('books/', views.book_list, name='book_list'),
    path('books/<int:id>/', views.book_detail, name='book_detail'),
]

# myproject/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),
]
```

## Templates

HTML templates:

```html
<!-- templates/books.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Books</title>
</head>
<body>
    <h1>Books</h1>
    <ul>
    {% for book in books %}
        <li>{{ book.title }} by {{ book.author }}</li>
    {% endfor %}
    </ul>
</body>
</html>
```

## Admin Interface

```python
# myapp/admin.py
from django.contrib import admin
from .models import Book

admin.site.register(Book)

# Create superuser
# python manage.py createsuperuser
```

## Forms

```python
# myapp/forms.py
from django import forms
from .models import Book

class BookForm(forms.ModelForm):
    class Meta:
        model = Book
        fields = ['title', 'author', 'published_date', 'price']
```

## Static Files

```python
# settings.py
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / "static"]
```

```html
<!-- In template -->
{% load static %}
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

---

**Related:** [[Python Libraries and Frameworks]] | [[Python]] | [[Python Classes and Objects]]
