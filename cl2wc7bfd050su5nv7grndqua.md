# 4- Write a view

Open the file polls/views.py For example, we open "Sublime Text" software. From File&gt;New Folder&gt; we select: PollProject floder

Then put the following Python code in polls/views.py:

```plaintext
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, visiter. You're at the polls project.")
```

To call the view, we need to map it to a URL.

In the polls directory, create a file called urls.py select: polls&gt;right click&gt; New File&gt; Save as&gt; urls.py

In the polls/urls.py file include the following code:

```plaintext
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

Then open: PollProject/urls.py and past the following code in it: \`\`\` from django.contrib import admin from django.urls import include, path

urlpatterns = \[ path('polls/', include('polls.urls')), path('admin/', admin.site.urls), \] `Verify it’s working with the following command:` py manage.py runserver \`\`\`

Then, go to http://localhost:8000/polls/ in your browser.