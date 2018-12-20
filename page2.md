# Taking Django to the SPA

### Contents:
* [Using Angular with Django](https://github.com/wgoode3/djangular/blob/master/page1.md)
* Taking Django to the SPA
* [Connecting Angular + Middleware Settings](https://github.com/wgoode3/djangular/blob/master/page3.md)
* [Getting and Posting data to our Django server](https://github.com/wgoode3/djangular/blob/master/page4.md)
* [Assignment 1 - Django Angular Tasks](https://github.com/wgoode3/djangular/blob/master/page5.md)
* [Using a database other than SQLite (Optional)](https://github.com/wgoode3/djangular/blob/master/page6.md)
* [Assignment 2 - Django Angular Login and Registration](https://github.com/wgoode3/djangular/blob/master/page7.md)
* [Assignment 3 - Django Angular E-Commerce (Highly Optional)](https://github.com/wgoode3/djangular/blob/master/page8.md)

By default, Django wants us to create multiple templates (html files with embedded python) for the server to render to our users. If instead we would like to create a **S**ingle **P**age **A**pplication we will have to play around with the settings somewhat. Enter [django-spa](https://github.com/metakermit/django-spa).
Django SPA is a middleware that will make it easy for us to make Django serve up our ```index.html``` for us.

### Before we get started, make sure you have all of the following installed:
* [Python 3.5 or newer](https://www.python.org/downloads/)
* [Virtualenv](https://virtualenv.pypa.io/en/latest/installation/)
* [Node.js](https://nodejs.org/en/download/)
* [Angular CLI](https://cli.angular.io/)
  ```shell
  # you should be able to run the following
  $ npm i -g @angular/cli
  # if you receive errors relating to permissions try sudo
  $ sudo npm i -g @angular/cli
  ```

### Let's start out by creating a new virtual environment and installing Django along with Django SPA.

```shell
virtualenv venv -p python3
source venv/bin/activate
pip install django django-spa
```

Then proceed to make a new project as normal, I would suggest this folder structure for now. If for instance we are making a project called ```papaya``` we would run ```django-admin startproject papaya```. Then inside of the first ```/papaya``` folder we could run ```python manage.py startapp papaya_app```. We will also want to create our angular app here as well with ```ng new client --routing```.

```
├─ papaya
┊ ├─ client
┊ ┊ ├─ e2e
┊ ┊ ├─ node_modules
┊ ┊ ├─ src
┊ ┊ ├─ angular.json
┊ ├─ papaya
┊ ┊ ├─ settings.py
┊ ┊ ├─ urls.py
┊ ├─ papaya_app
┊ ┊ ├─ models.py
┊ ┊ ├─ views.py
├─ venv
        
# some files and folders removed for brevity
```

[Next](https://github.com/wgoode3/djangular/blob/master/page3.md)