----
## Class-Based Views

[Resource](https://docs.djangoproject.com/en/4.0/topics/class-based-views/intro/)

#### Why use it?

*CBVs* introduce to *solve problems of FBVs* : **repeating** same patterns again and again such as lists all objects in a model, etc.

Django introduced *Class-Based generic views (CBGVs)* to extend views covering common use cases.

----

At first, there was only function contract: [`HttpRequest`](https://docs.djangoproject.com/en/4.0/ref/request-response/#django.http.HttpRequest) -> Function -> [`HttpResponse`](https://docs.djangoproject.com/en/4.0/ref/request-response/#django.http.HttpResponse).
We see some patterns from view development. so [Function-based generic views](https://medium.com/@ksarthak4ever/django-class-based-views-vs-function-based-view-e74b47b2e41b) were introduced
- Problems of FBGVs : no ways to extend or customize.

```python
from django.shortcuts import render, redirect
from .models import Post

def delete_post(request, pk):
    post = Post.objects.get(pk=pk)
    if request.method == 'POST':
        post.delete()
        return redirect('post_list')
    return render(request, 'blog/post_confirm_delete.html', {'post': post})
```

[[Example of FBVs|MORE EXAMPLE]]

----

#### Core

CBVs allows us *to response to different* [HTTP request methods](https://softuni.org/dev-concepts/everything-you-need-to-know-about-http-protocol/) with *different class instance* instead of branching code in single view function.

From this
```python
from django.http import HttpResponse

def my_view(request):
    if request.method == 'GET':
        # <view logic>
        return HttpResponse('result')
```

To this
```python
from django.http import HttpResponse
from django.views import View

class MyView(View):
    def get(self, request):
        # <view logic>
        return HttpResponse('result')
```

Anyway, Django's URL resolver want us to send request and associated arguments to a callable function, not a class.

We will use [as_view()](https://docs.djangoproject.com/en/4.0/ref/class-based-views/base/#django.views.generic.base.View.as_view) method to return a callable view that takes a request and returns a response.

```python
# urls.py
from django.urls import path
from myapp.views import MyView

urlpatterns = [
    path('about/', MyView.as_view()),
]
```

##### What happen when the view is called?
- [`setup()`](https://docs.djangoproject.com/en/4.0/ref/class-based-views/base/#django.views.generic.base.View.setup) method assigns (Initialize Its attributes) the [`HttpRequest`](https://docs.djangoproject.com/en/4.0/ref/request-response/#django.http.HttpRequest) to view's request attribute
- Any keyword arguments [captured from the URL pattern](https://docs.djangoproject.com/en/4.0/topics/http/urls/#how-django-processes-a-request) to the `args`, `kwargs` attributes
- Then, [`dispatch()`](https://docs.djangoproject.com/en/4.0/ref/class-based-views/base/#django.views.generic.base.View.dispatch) (determine whether it is a `GET` or `POST`) is called
- Raise [`HttpResponseNotAllowed`](https://docs.djangoproject.com/en/4.0/ref/request-response/#django.http.HttpResponseNotAllowed "django.http.HttpResponseNotAllowed") if not defined.

**NOTE:** Its return some form of [`HttpResponse`](https://docs.djangoproject.com/en/4.0/ref/request-response/#django.http.HttpResponse "django.http.HttpResponse") like a FBVs.

#### Configure the class attributes
1. Subclassing and overriding attributes and methods
```python
from django.http import HttpResponse
from django.views import View

class GreetingView(View):
	greeting = "Good Day"
	
	def get(self, request):
		return HttpResponse(self.greeting)

class MorningGreetingView(GreetingView):
	greeting = "Morning to ya"
```

2. Configure using `kwargs` to the `as_view()` call in the URLconf.
```python
urlpatterns = [
	path('about/', 
	GreetingView.as_view(greeting='Gday'))
]
```
