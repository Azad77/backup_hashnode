# 9- Writing more views

In our poll application, we’ll have the following four views:

Question “index” page – displays the latest few questions.
Question “detail” page – displays a question text, with no results but with a form to vote.
Question “results” page – displays results for a particular question.
Vote action – handles voting for a particular choice in a particular question.

Add mentioned views to polls/views.py
```
def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```
Connet these new views into the polls/urls.py by adding the following path() calls:
```
from django.urls import path

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
To display the latest 5 poll questions in the system, edit polls/view.py to be:
```
from django.http import HttpResponse
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

