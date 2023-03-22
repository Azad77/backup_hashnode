---
title: "9- How to Add Four Essential Views to Your Poll Application"
datePublished: Sun May 08 2022 14:28:55 GMT+0000 (Coordinated Universal Time)
cuid: cl2xe4uoi003zrgnvcinb3m85
slug: 9-how-to-add-four-essential-views-to-your-poll-application
tags: django, web-development

---

Poll applications are a popular way to gather opinions and insights from a large group of people. However, to make a poll application truly useful, you need to have the right views in place. In this article, we will walk you through the process of adding four essential views to your poll application: the question index page, the question detail page, the question results page, and the vote action. By the end of this tutorial, you'll have a fully functional poll application with multiple views that users can interact with. So, let's dive in and get started!

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

```python
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

Congratulations! You've now added four essential views to your poll application, making it more user-friendly and functional. Users can now browse questions, view details, see results, and vote on their favorite options. Of course, there are many other features you could add to your poll application, such as authentication, pagination, or search. But with these four views, you have a solid foundation to build on. We hope you found this tutorial helpful and informative. If you have any questions or feedback, please let us know.

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.