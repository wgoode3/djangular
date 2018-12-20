# Using a database other than SQLite (Optional)

### Contents:
* [Using Angular with Django](https://github.com/wgoode3/djangular/blob/master/page1.md)
* [Taking Django to the SPA](https://github.com/wgoode3/djangular/blob/master/page2.md)
* [Connecting Angular + Middleware Settings](https://github.com/wgoode3/djangular/blob/master/page3.md)
* [Getting and Posting data to our Django server](https://github.com/wgoode3/djangular/blob/master/page4.md)
* [Assignment 1 - Django Angular Tasks](https://github.com/wgoode3/djangular/blob/master/page5.md)
* Using a database other than SQLite (Optional)
* [Assignment 2 - Django Angular Login and Registration](https://github.com/wgoode3/djangular/blob/master/page7.md)
* [Assignment 3 - Django Angular E-Commerce (Highly Optional)](https://github.com/wgoode3/djangular/blob/master/page8.md)

While SQLite is a very convenient database when developing, your project might benefit from a different database. In Django changing the database can be very easy to do, and we'll include examples for how you might do that.

### Mongo

If you want to connect to a Mongo database using Django, the easiest way might be [Djongo](https://nesdis.github.io/djongo/).

First we need to install the ```djongo``` package using pip. Make sure your virtualenvironment is active.

```shell
pip install djongo
```

Then we will modify the ```DATABASE``` setting in the ```settings.py``` accordingly.

```python
# Replace the DATABASE setting with this...
DATABASES = {
    'default': {
        'ENGINE': 'djongo',
        'NAME': 'amazing_tasks'
    }
}
```

That's it. Assuming mongodb is running, it will create a ```db``` called 'amazing_tasks' and connect to it. You can continue to use the Django ORM as you have previously.

### MySQL

Connecting to a MySQL database will be a little bit more involved. These instructions will assume you are using it during deployment to an Ubuntu server.

Make sure your virtualenvironment is active

```shell
sudo apt-get install python3-dev
sudo apt-get install python3-dev libmysqlclient-dev
sudo apt-get install mysql-server
pip install mysqlclient
mysql -u root -p
# enter your password (root) when prompted
create schema amazing_tasks;
exit
```

Then we will modify the ```DATABASE``` setting in the ```settings.py``` accordingly.

```python
# Replace the DATABASE setting with this...
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'amazing_tasks',
        'USER': 'root',
        'PASSWORD': 'root',
        'HOST': 'localhost',
        'PORT': '3306',
    }
} 
```

You may need to adjust the values of ```USER``` and ```PASSWORD``` accordingly. Make sure the ```NAME``` is the same as the name of the schema you created in MySQL above.

[Next](https://github.com/wgoode3/djangular/blob/master/page7.md)