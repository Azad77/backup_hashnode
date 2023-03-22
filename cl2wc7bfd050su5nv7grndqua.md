---
title: "4- How to Map Views to URLs in Django"
datePublished: Sat May 07 2022 20:47:05 GMT+0000 (Coordinated Universal Time)
cuid: cl2wc7bfd050su5nv7grndqua
slug: 4-how-to-map-views-to-urls-in-django
tags: django, web-development

---

In this article, you will learn how to map views to URLs in Django. We will guide you through the process step by step, starting from opening the necessary files in Sublime Text to verifying that everything is working correctly in your browser. By following these instructions, you will be able to create a functional web application using Django.

Open the file `polls/views.py`. For example, open the "Sublime Text" software and select `File > New Folder`. Then, select the `PollProject` folder.

Next, paste the following Python code in `polls/views.py`:

```python
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, visitor. You're at the polls project.")
```

To call the view, we need to map it to a URL. In the `polls` directory, create a file called [`urls.py`](http://urls.py) by selecting `polls > right click > New File > Save as >` [`urls.py`](http://urls.py).

In the `polls/urls.py` file, include the following code:

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

Then open PollProject/urls.py and paste the following code into it:

```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```

Verify that it is working by running the following command: `python` [`manage.py`](http://manage.py) `runserver`.

Finally, open your browser and go to [**http://localhost:8000/polls/**](http://localhost:8000/polls/).

In conclusion, this article provides a step-by-step guide on how to map views to URLs in Django. By following the instructions provided, you can create a functional web application using Django. The article also includes code snippets and commands to run to verify that everything is working correctly.

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.