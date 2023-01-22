# 7- Create a new question and choices

To invoke the Python shell, use this command:
```
py manage.py shell
```
Once you’re in the shell:
```
from polls.models import Choice, Question
```
Create a new Question.
```
from django.utils import timezone
q = Question(question_text="Rate this tutorial:", pub_date=timezone.now())
```

Save the object into the database. You have to call save() explicitly.
```
q.save()
```
Now it has an ID.
```
q.id
#1
```
Access model field values via Python attributes.
```
q.question_text
```
'Rate this tutorial:'
```
q.pub_date
```
datetime.datetime(2022, 5, 14, 15, 41, 26, 711723, tzinfo=datetime.timezone.utc)

Create five choices:
```
q.choice_set.create(choice_text='*', votes=0)
q.choice_set.create(choice_text='**', votes=0)
q.choice_set.create(choice_text='***', votes=0)
q.choice_set.create(choice_text='****', votes=0)
q.choice_set.create(choice_text='*****', votes=0)

q.choice_set.all()
```