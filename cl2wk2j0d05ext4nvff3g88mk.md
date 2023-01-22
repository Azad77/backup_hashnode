# 5- Database setup

Open up PollProject/settings.py. By default, the configuration uses SQLite.

Inside PollProject/settings.py, set TIME\_ZONE to your time zone. For example, in my case, it be: `TIME_ZONE = 'Asia/Baghdad'`

To create the tables in the database we run the following command:

```plaintext
py manage.py migrate
```