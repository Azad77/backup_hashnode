---
title: "4- Write a view"
datePublished: Sat May 07 2022 20:47:05 GMT+0000 (Coordinated Universal Time)
cuid: cl2wc7bfd050su5nv7grndqua
slug: 4-write-a-view
tags: django, web-development

---

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

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.