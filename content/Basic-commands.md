---
title: Basic Commands
---

Here are the list of commands to use in Django.
#### Some Basic Commands

[Run server](https://docs.djangoproject.com/en/4.2/ref/django-admin/#runserver)
`python manage.py runserver <port: default=8000>`

----

[Create new Django project](https://docs.djangoproject.com/en/4.2/ref/django-admin/#startproject)
`django-admin startproject <project name> <directory>`
*or*
`python -m django startproject <project name>`

[Create new apps](https://docs.djangoproject.com/en/4.2/ref/django-admin/#startapp)
`python manage.py startapp <name> <directory>`

----

[Migration](https://docs.djangoproject.com/en/4.2/topics/migrations/) : propagating changes you make to your models (adding a field, deleting a model, etc.) -> You should think of migrations as a *version control system for your database schema*

`makemigrations` is responsible for *packaging up your model changes into individual migration files* - analogous to commits - and `migrate` is responsible for *applying those to your database*.

`makemigrations = commits` 

1. [migrate](https://docs.djangoproject.com/en/4.2/ref/django-admin/#migrate) : Sync the database state with the current set of models and migrations
`python manage.py migrate [app_label] [migrate_name]`
``
2. [makemigrations](https://docs.djangoproject.com/en/4.2/ref/django-admin/#makemigrations): Create new migrations on the change detect on models.
`python manage.py makemigrations [app_label [app_label ...]]`

3.  [showmigrations](https://docs.djangoproject.com/en/4.2/ref/django-admin/#showmigrations): Show all migrations in project.
``python manage.py showmigrations [app_label [app_label ...]]``

----

[Shell](https://docs.djangoproject.com/en/4.2/ref/django-admin/#shell)

``django-admin shell``
*or*
`python manage.py shell`

`--interface` `{ipython,bpython,python}, -i` `{ipython,bpython,python}

[test](https://docs.djangoproject.com/en/4.2/ref/django-admin/#test)
``python manage.py test [test_label [test_label ...]]``

----

These commands are only available if Django’s [authentication system](https://docs.djangoproject.com/en/4.2/topics/auth/) (`django.contrib.auth`) is installed.

[changepassword](https://docs.djangoproject.com/en/4.2/ref/django-admin/#changepassword)
``django-admin changepassword [<username>]``

[createsuperuser](https://docs.djangoproject.com/en/4.2/ref/django-admin/#createsuperuser)
`django-admin createsuperuser`