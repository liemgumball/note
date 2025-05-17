Created: April 1, 2023 6:14 PM
Class: Self-Research
Type: Back-end
Materials: https://www.w3schools.com/django/, https://youtu.be/i5JykvxUk_A
Reviewed: Yes
Edited: July 18, 2024 2:52 PM

# Setup file env & work

```bash
python -m venv env
source env/bin/activate
```

### Installation

```bash

pip install -r requirements

# Or
pip install djangorestframework
pip install markdown       # Markdown support for the browsable API.
pip install django-filter  # Filtering support
```

To update `requirements.txt`

```bash
pip freeze > requirements.txt
```

Run to create a project

```bash
django-admin startproject 'project-name'
```

Create app

```bash
cd 'project-name' && python manage.py startapp 'app-name'
```

Create view and database by coding

> In Django, data is created in objects, called Models, and is actually tables in a database.
> 

```python
#in app/models.py
from django.db import models

class Member(models.Model):
  firstname = models.CharField(max_length=255)
  lastname = models.CharField(max_length=255)
```

Run this to create database

```bash
python manage.py makemigrations 'app-name'
python manage.py migrate
#run shell to see data record
python manage.py shell
>>>.....
```

Also can modifier add Fields in the Model

```python
from django.db import models

class Member(models.Model):
  firstname = models.CharField(max_length=255)
  lastname = models.CharField(max_length=255)
  phone = models.IntegerField()
  joined_date = models.DateField()
```

We can display all data by using View and Prepare Templates or using Admin User of Django

```bash
python manage.py createsuperuser
```

---

# REST Framework

import ‘rest_framework’ into INSTALLED_APPS in file setting.py

Create a `serializers.py` file to make an API

> Use ‘from rest_framework import Response’ so we can get correctly (between Json or HTML)
> 

Use @api_view to define what kind of API we want (GET, POST, PUT, DELETE)

## Test API

- Pip install request in Python and write code to test API

```python
import request
response = request.get('http://127.0.0.1:8000/testing')
print(response)
```

- Using testing app **Postman** to test API

# REST-Swagger

- View the page of all of the APIs

```bash
pip install drf-yasg
```