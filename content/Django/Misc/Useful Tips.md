### Apps

#### Django doesn't know about new app until we tell it

We explicitly add it to the `django_project/settings.py` 

```python
# django_project/settings.py
INSTALLED_APPS = [
"django.contrib.admin",
"django.contrib.auth",
"django.contrib.contenttypes",
"django.contrib.sessions",
"django.contrib.messages",
"django.contrib.staticfiles",
"pages.apps.PagesConfig", # new
]
```

What is **PagesConfig** -> represents an app for a Django project, including metadata such as name, label and path.

```python
# pages/apps.py
from django.apps import AppConfig

class PagesConfig(AppConfig):
default_auto_field = "django.db.models.BigAutoField"
name = "pages"
```

#### Don't forgot to configure our URLs in project and apps

Our URL pattern has three parts:
1. a Python regular expression
2. a reference to the view
3. an optional [named URL pattern](https://docs.djangoproject.com/en/4.0/topics/http/urls/#naming-url-patterns)in order to perform [URL reversing](https://docs.djangoproject.com/en/4.2/ref/urlresolvers/)

More about [URL reversing](https://docs.djangoproject.com/en/4.0/topics/http/urls/#reverse-resolution-of-urls)

Here is example of `apps/urls.py`

APP
```python
# pages/urls.py
from django.urls import path
from .views import homePageView # FBVs
from .views import HomePage

urlpatterns = [
	path("", homePageView, name="home"), # FBVs
	path("home/" HomePage.as_view(), name="home2"), # CBVs
]

```
PROJECT 
```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
	path("admin/", admin.site.urls),
	path("", include("pages.urls")), # new
]
```

