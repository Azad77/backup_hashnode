---
title: "10- Create templates"
datePublished: Sun May 08 2022 15:33:20 GMT+0000 (Coordinated Universal Time)
cuid: cl2xgfoo300b6rgnv1q1z8xkb
slug: 10-create-templates
tags: django, web-development, template

---

Creating custom templates is an essential step in developing a Django web application. Not only does it help improve the overall user experience, but it also plays a crucial role in optimizing your app's search engine rankings. In this article, we'll take you through a step-by-step guide on how to create custom templates in Django. So, let's get started!

First, create a directory called "templates" in your "polls" directory. Django will look for templates in there.

In "Sublime Text": select "polls" &gt; right-click &gt; New Folder &gt; name it "templates"

Within the "templates" directory, create another directory called "polls", and within that, create a file called "index.html".

Select "polls" folder inside "templates" folder &gt; right-click &gt; New File &gt; Save as: "index.html"

Then, put the following code in that template:

```python
{% if latest_question_list %}
    <ul>
    {% for question in latest_question_list %}
        <li><a href="/polls/{{ question.id }}/">{{ question.question_text }}</a></li>
    {% endfor %}
    </ul>
{% else %}
    <p>No polls are available.</p>
{% endif %}
```

Then, update our "index" view in "polls/views.py" to use the template:

```python
from django.http import HttpResponse
from django.template import loader

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = {
        'latest_question_list': latest_question_list,
    }
    return HttpResponse(template.render(context, request))

def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```

Now, open [**http://127.0.0.1:8000/polls/**](http://127.0.0.1:8000/polls/) in your browser.

Inside "polls" directory in "templates", create "detail.html" and write the following code in it:

```python
<h1>{{ question.question_text }}</h1>
<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }}</li>
{% endfor %}
</ul>
```

Add a shortcut, "get\_object\_or\_404()", to "polls/views.py":

```python
from django.shortcuts import get_object_or_404, render

from .models import Question
# ...
def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})
```

To remove hardcoded URLs in templates, edit "polls/index.html" to:

```python
<li><a href="{% url 'detail' question.id %}">{{ question.question_text }}</a></li>
```

So, "index.html" should be like:

```python
{% if latest_question_list %}
    <ul>
    {% for question in latest_question_list %}
        <li><a href="{% url 'detail' question.id %}">{{ question.question_text }}</a></li>
    {% endfor %}
    </ul>
{% else %}
    <p>No polls are available.</p>
{% endif %}
```

By using best practices such as avoiding hardcoded URLs and utilizing shortcuts like "get\_object\_or\_404()", you can create templates that are both efficient and effective. With this knowledge, you can take your Django app to the next level and provide your users with a seamless experience.

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.