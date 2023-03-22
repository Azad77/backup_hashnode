---
title: "9- Writing more views"
datePublished: Sun May 08 2022 14:28:55 GMT+0000 (Coordinated Universal Time)
cuid: cl2xe4uoi003zrgnvcinb3m85
slug: 9-writing-more-views
tags: django, web-development

---

In our poll application, we will have the following four views:

1. Question "index" page - displays the latest few questions.
    
2. Question "detail" page - displays a question text, with no results but with a form to vote.
    
3. Question "results" page - displays results for a particular question.
    
4. Vote action - handles voting for a particular choice in a particular question.
    

Add the mentioned views to polls/views.py:

```python
pythonCopy codefrom django.http import HttpResponse
from .models import Question

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5] 
    output = ', '.join([q.question_text for q in latest_question_list])
    return HttpResponse(output)

def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```

Connect these new views into the polls/urls.py by adding the following path() calls:

```
javascriptCopy codefrom django.urls import path
from . import views

urlpatterns = [
    # ex: /polls/
    path('', views.index, name='index'),
    # ex: /polls/5/
    path('<int:question_id>/', views.detail, name='detail'),
    # ex: /polls/5/results/
    path('<int:question_id>/results/', views.results, name='results'),
    # ex: /polls/5/vote/
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```

To display the latest 5 poll questions in the system, edit polls/views.py to be:

```
pythonCopy codefrom django.http import HttpResponse
from .models import Question

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5] 
    output = ', '.join([q.question_text for q in latest_question_list])
    return HttpResponse(output)

def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.