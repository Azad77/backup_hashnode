# 5- Database setup

Open up PollProject/settings.py. By default, the configuration uses SQLite.

Inside PollProject/settings.py, set TIME\_ZONE to your time zone. For example, in my case, it is: `TIME_ZONE = 'Asia/Baghdad'`

```python
py manage.py migrate
```

If you like the content, please [SUBSCRIBE](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) to my channel for the future content

To create the tables in the database we run the following command: