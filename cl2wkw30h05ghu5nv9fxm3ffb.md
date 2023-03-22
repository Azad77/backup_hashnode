---
title: "6- Creating Models for a Poll App with Django."
datePublished: Sun May 08 2022 00:50:17 GMT+0000 (Coordinated Universal Time)
cuid: cl2wkw30h05ghu5nv9fxm3ffb
slug: 6-creating-models-for-a-poll-app-with-django
tags: django

---

Learn how to create models for a poll app with Django by following the step-by-step guide provided in this article. You'll create two models, Question and Choice, and edit the polls/models.py file to add the necessary code. Then, you'll edit the PollProject/settings.py file to add the dotted path to the INSTALLED\_APPS setting. Finally, you'll run a few commands to create the model tables in your database. By the end of this tutorial, you'll have a fully functional poll app that you can use for your own projects.

In our poll app, we will create two models: Question and Choice. Please edit the polls/models.py file so that it looks like the following:

```python
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

Next, edit the PollProject/settings.py file and add the dotted path to the INSTALLED\_APPS setting. It should look like this:

```python
INSTALLED_APPS = [
    'polls.apps.PollsConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

Let's run another command:

```python
python manage.py makemigrations polls
```

You should see output like this:

```python
BEGIN;
--
-- Create model Question
--
CREATE TABLE "polls_question" (
    "id" serial NOT NULL PRIMARY KEY,
    "question_text" varchar(200) NOT NULL,
    "pub_date" timestamp with time zone NOT NULL
);
--
-- Create model Choice
--
CREATE TABLE "polls_choice" (
    "id" serial NOT NULL PRIMARY KEY,
    "choice_text" varchar(200) NOT NULL,
    "votes" integer NOT NULL,
    "question_id" integer NOT NULL
);
ALTER TABLE "polls_choice"
  ADD CONSTRAINT "polls_choice_question_id_c5b4b260_fk_polls_question_id"
    FOREIGN KEY ("question_id")
    REFERENCES "polls_question" ("id")
    DEFERRABLE INITIALLY DEFERRED;
CREATE INDEX "polls_choice_question_id_c5b4b260" ON "polls_choice" ("question_id");

COMMIT;
```

To create those model tables in your database, run the following migrate command:

```python
python manage.py migrate
```

You should see output like this:

```python
Operations to perform: Apply all migrations: admin, auth, contenttypes, polls, sessions Running migrations: Applying polls.0001_initial... OK Inside polls/models.py add a __str__() method to both Question and Choice: class Question(models.Model): # ... def str(self): return self.question_text

class Choice(models.Model): # ... def str(self): return self.choice_text Under class Question(models.Model) add: def was_published_recently(self): now = timezone.now() return now - datetime.timedelta(days=1) <= self.pub_date <= now was_published_recently.admin_order_field = 'pub_date' was_published_recently.boolean = True was_published_recently.short_description = 'Published recently?'
```

Now, polls/models.py should look like this:

```python
import datetime

from django.db import models
from django.utils import timezone


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

    def __str__(self):
        return self.question_text

    def was_published_recently(self):
        now = timezone.now()
        return now - datetime.timedelta(days=1) <= self.pub_date <= now
    was_published_recently.admin_order_field = 'pub_date'
    was_published_recently.boolean = True
    was_published_recently.short_description = 'Published recently?'


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def __str__(self):
        return self.choice_text
```

In conclusion, this article provides a step-by-step guide on how to create models for a poll app with Django. By following the instructions provided, readers can create two models, Question and Choice, and add the necessary code to the polls/models.py file. They can also edit the PollProject/settings.py file to add the dotted path to the INSTALLED\_APPS setting and run a few commands to create the model tables in their database. By the end of the tutorial, readers will have a fully functional poll app that they can use for their own projects.

If you find this content helpful, please consider [subscribing](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for future updates.