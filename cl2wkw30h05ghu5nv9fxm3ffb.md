# 6- Creating models

In our poll app, we’ll create two models: Question and Choice. Edit the polls/models.py file so it looks like this: \`\`\` from django.db import models

class Question(models.Model): question\_text = models.CharField(max\_length=200) pub\_date = models.DateTimeField('date published')

class Choice(models.Model): question = models.ForeignKey(Question, on\_delete=models.CASCADE) choice\_text = models.CharField(max\_length=200) votes = models.IntegerField(default=0) \`\`\`

Edit the PollProject/settings.py file and add that dotted path to the INSTALLED\_APPS setting. It’ll look like this:

```plaintext
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

## Let’s run another command: `py manage.py makemigrations polls` You should see: `Migrations for 'polls': polls\migrations\0001_initial.py - Create model Question - Create model Choice` Then run sqlmigrate command: `py manage.py sqlmigrate polls 0001` You should see something like this: \`\`\` BEGIN;

## \-- Create model Question

## CREATE TABLE "polls\_question" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "question\_text" varchar(200) NOT NULL, "pub\_date" datetime NOT NULL);

## \-- Create model Choice

CREATE TABLE "polls\_choice" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "choice\_text" varchar(200) NOT NULL, "votes" integer NOT NULL, "question\_id" bigint NOT NULL REFERENCES "polls\_question" ("id") DEFERRABLE INITIALLY DEFERRED); CREATE INDEX "polls\_choice\_question\_id\_c5b4b260" ON "polls\_choice" ("question\_id"); COMMIT; `To create those model tables in your database, run migrate command:` py manage.py migrate `You should see something like:` Operations to perform: Apply all migrations: admin, auth, contenttypes, polls, sessions Running migrations: Applying polls.0001\_initial... OK `Inside polls/models.py add a __str__() method to both Question and Choice:` class Question(models.Model): # ... def **str**(self): return self.question\_text

class Choice(models.Model): # ... def **str**(self): return self.choice\_text `Under class Question(models.Model) add:` def was\_published\_recently(self): now = timezone.now() return now - datetime.timedelta(days=1) &lt;= self.pub\_date &lt;= now was\_published\_recently.admin\_order\_field = 'pub\_date' was\_published\_recently.boolean = True was\_published\_recently.short\_description = 'Published recently?' `Now, polls/models.py should be like that:` import datetime

from django.db import models from django.utils import timezone

class Question(models.Model): question\_text = models.CharField(max\_length=200) pub\_date = models.DateTimeField('date published')

def **str**(self): return self.question\_text

def was\_published\_recently(self): now = timezone.now() return now - datetime.timedelta(days=1) &lt;= self.pub\_date &lt;= now was\_published\_recently.admin\_order\_field = 'pub\_date' was\_published\_recently.boolean = True was\_published\_recently.short\_description = 'Published recently?'

class Choice(models.Model): question = models.ForeignKey(Question, on\_delete=models.CASCADE) choice\_text = models.CharField(max\_length=200) votes = models.IntegerField(default=0)

def **str**(self): return self.choice\_text \`\`\`