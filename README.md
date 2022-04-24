# django


```python
__init__.py
```
It only serves us to mark the folder as python module. This is not django exclusive concept

Create new django project:

```shell
django-admin startproject project_name
```

How to run django server

```python
python3 manage.py runserver
```

Modules in django are called apps.

Apps, what are they? <br>
We can see them as features. Building blocks that form this overall project.

Example: Online shop is a project, apps are Producrs, Cart, Admin Area

https://github.com/academind/django-practical-guide-course-code/tree/setup-zz-extra-files

To create new django app, we run command

```shell
python3 manage.py startapp app_name
```

We have to make django be aware of newly created app by adding it to INSTALLED_APPS in global setting.py file

```python
INSTALLED_APPS = [
    'blog',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

### URL&Views

We have to addd urls.py file in each app folder.

Slug urls are SEO friendly because they describe a reached page in a way

When defining a slug url, django offers this buit in slug transformer.

```python
path("posts/<slug: slug>") # /posts/my-first-post
```
This does one main thing, it check if this concrete value which is passed when this path is reached has this slug format. Basically it means it's some text that contains characters and numbers and may contain dashes, but it doesn't contain any other special characters.

Functions that are triggered when this url is reached are called view functions and they are stored in views.py file.

In view functions request parametar is passed automatically by django, but we have to put it in function definition
```python
def starting_page(request):
    pass
```

Naming each path in url file is common practice, because we are going to nned does urls later in the code and it is better if we can reference them through their  name, so that the paths itself can change in the future in only one place

```python
urlpatterns=[
    path("", views.starting_page, name="starting-page"),
    path("posts", views.posts, name="posts-page"),
    path("posts/<slug: slug>", views.single_post, name="post-detail-page")
]
```

we have to wire up those urls in the project wide urls. We do that in urls.py from the project root. for that we need this include function which we include form django.urls.

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path("", include("blog.urls"))
]
```


### Templates

There is a django extension for VS code that can highlight django template language.<br>
we are adding templates folder in each app. In there it is best practise to repeat app folder name.<br>
We can also add a global templates folder for base templates - templates we want to use everywhere in the app, which the other templates will inherit.

We use block option in django template language to leave a place where any template can plug in into base template by leaving dedicated place for it

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %} {% endblock %}</title>
    {% block css_files %} {% endblock %}
</head>
<body>
    {% block content %} {% endblock %}
</body>
</html>
```

We inherit the base html by adding extends tag. 

```html
{% extends  "base.html" %}

{% block title%}
    My blog
{% endblock %}

{% block content%}
    <h1>Welcome to my blog</h1>
{% endblock %}
```


If we are inheriting from global templates folder we have to tell django to evaluate this global templates folder.

In settings.py file we add, which construct django to consider this ase templates folder when it is looking form templates

```python
TEMPLATES=[
    {
        'DIRS':[
            BASE_DIR / "templates"
        ]
    }
]
```

Without this, this extends statement in html template would fail

(templates foders in app files are consider because django is aware of the all added apps, when we added them to INSTALLED_APPS list)

And finally this is how we instruct django to render a template for a certain view

```python
def starting_page(request):
    return render(request, "blog/index.html")
```

Behind this render function django actually returns an HttpResponse object.





