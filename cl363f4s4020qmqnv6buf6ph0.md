---
title: "7- How to Create a Django Model with Questions and Choices"
datePublished: Sat May 14 2022 16:38:54 GMT+0000 (Coordinated Universal Time)
cuid: cl363f4s4020qmqnv6buf6ph0
slug: 7-how-to-create-a-django-model-with-questions-and-choices
tags: django, web-development, poll

---

In this article, we'll show you how to create a Django model with questions and choices. You'll learn how to use the Python shell to create and save a new question object in the database, access model field values using Python attributes, and create multiple choices for your question. Follow along with our step-by-step guide to get started with Django models and build your own interactive web applications.

To invoke the Python shell, use this command:

```python
py manage.py shell
```

Once you’re in the shell:

```python
from polls.models import Choice, Question
```

Create a new Question.

```python
from django.utils import timezone
q = Question(question_text="Rate this tutorial:", pub_date=timezone.now())
```

Save the object into the database. You have to call save() explicitly.

```python
q.save()
```

Now it has an ID.

```python
q.id
#1
```

Access model field values via Python attributes.

```python
q.question_text
```

'Rate this tutorial:'

```python
q.pub_date
```

datetime.datetime(2022, 5, 14, 15, 41, 26, 711723, tzinfo=datetime.timezone.utc)

Create five choices:

```python
q.choice_set.create(choice_text='*', votes=0)
q.choice_set.create(choice_text='**', votes=0)
q.choice_set.create(choice_text='***', votes=0)
q.choice_set.create(choice_text='****', votes=0)
q.choice_set.create(choice_text='*****', votes=0)

q.choice_set.all()
```

In conclusion, this article provides a step-by-step guide on how to create a Django model with questions and choices. It demonstrates how to use the Python shell to create and save a new question object in the database, access model field values using Python attributes, and create multiple choices for the question. By following this guide, readers can get started with Django models and build their own interactive web applications.

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.