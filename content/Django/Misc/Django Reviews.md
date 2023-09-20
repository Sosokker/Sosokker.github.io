----

#### Materials

- [[Basic commands]]
- [[Useful Tips]]

----
#### MVTU components of Django

- **Model** : Manage data and core business logic
- **View**: Describe which data to sent to user but not its presentation.
- **Template**: Presents data as HTML with optional CSS, JS and Static Assets
- **URL Configuration**: Regular-expression components configured to a **View**

**Traditional HTTP flow**
HTTP Request -> URLs -> Django combines database, logic, styling -> HTTP Response

**Django HTTP flow**
	HTTP Request -> URLs -> View -> Model and Templates -> HTTP Response

---

#### Basic File structure of Django Project

```
├── django_project
│ ├── __init__.py
| ├── asgi.py
│ ├── settings.py
│ ├── urls.py
│ └── wsgi.py
├── manage.py
└── .venv/
```

1. `__init__.py` to tell python that the files in the folder are part of a Python package. Without this file, we can't import files from another directory.
2. `asgi.py` allows for an optional [Asynchronous Server Gateway Interface](https://en.wikipedia.org/wiki/Asynchronous_Server_Gateway_Interface) to be run
3. `settings.py` controls our Django project's overall settings.
4. `urls.py` which page to build in response to the browser or URL request.
5. `wsgi.py` stands for [Web Server Gateway Interface](https://en.wikipedia.org/wiki/Web_Server_Gateway_Interface) which help Django server out eventual web pages

----
#### Basic File structure of "APP"

Django project can contain many apps -> Each app control isolated piece of functionality.

Note: In general, each app should have clear function

```
├── pages
│ ├── __init__.py
│ ├── admin.py
│ ├── apps.py
│ ├── migrations
│ │ └── __init__.py
│ ├── models.py
│ ├── tests.py
│ └── views.py
```

1. `admin.py` is a configuration file for built-in Django Admin app.
2. `apps.py` is a configuration file for app itself.
3. `migrations` keep track of any changes to our `models.py`
4. `models.py` is where we define out database models, then, Django will automagically translates into database table.
5. `tests.py` is where we define test for specific app
6. `views.py` is where we handle request/response logic for our web app.

----

#### Views

There are two types of view in Django :
1. **FBVs** : Function-Based views -> Simple to implement
2. **CBVs** : Class-Based views -> Allow for much greater code reusability.

In Class-Based view we can use **built-in generic class-based views** (**GCBVs**) to handle common use cases.

[[View |READ MORE]]

----

#### Templates
By default, Django's template loader will *look within each app for related templates*. However structure is somewhat confusing: *each app needs new templates directory* then other with same name as app and then those template file.

```
└── pages
	├── templates
		├── pages
			├── home.html
```

Why it is so repetitive *->* Django template loader wants to be really sure that it will find the correct template. *->* No conflict when 2 apps have same file name.

And *instead of* create a *single project-level templates directory* and place all templates within there, we can use other way to tell Django to *look in some directories for templates*

*Update the* `settings.py`

```python
# django_project/settings.py
TEMPLATES = [
{
	...
	"DIRS": [BASE_DIR / "templates"], # new
	...
},
]
```
