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

There is a django extension for VS code that can highlight django template language.


