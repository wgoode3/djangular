# Connecting Angular + Middleware Settings

<a href="https://youtu.be/8KoyisKqLlc" target="_blank">
	<img src="https://i.ytimg.com/vi/8KoyisKqLlc/hqdefault.jpg" alt="thumbnail">
</a>

### Start by editting our settings.py

```python
# make your list of installed apps look like this

INSTALLED_APPS = [
	'papaya_app',
	'django.contrib.contenttypes',
	'django.contrib.sessions',
	'django.contrib.messages',
	'django.contrib.staticfiles',
]

# and make your list of middleware look like this

MIDDLEWARE = [
	'django.middleware.security.SecurityMiddleware',
	'whitenoise.middleware.WhiteNoiseMiddleware',
	'django.contrib.sessions.middleware.SessionMiddleware',
	'django.middleware.common.CommonMiddleware',
	'spa.middleware.SPAMiddleware'
]

# add these lines at the bottom of the file

STATIC_ROOT = os.path.join(BASE_DIR, "client/dist/client/")
STATICFILES_STORAGE = 'spa.storage.SPAStaticFilesStorage'
```

Note that we have elected to skip the ```apps``` folder so we can simply add ```'papaya_app'``` to our list of installed apps. Also we removed a few unused apps, namely ```'django.contrib.admin'``` and ```'django.contrib.auth'```. Next be sure to add ```'whitenoise.middleware.WhiteNoiseMiddleware'``` and ```'spa.middleware.SPAMiddleware'``` to our list of middleware. Also we decided to remove a few unused middleware as we did above with the apps, namely ```'django.middleware.csrf.CsrfViewMiddleware'```, ```'django.contrib.auth.middleware.AuthenticationMiddleware'```, and ```'django.contrib.messages.middleware.MessageMiddleware'```.

Lastly be sure to add in ```STATIC_ROOT``` and point it to the ```dist``` folder in our angular app and also add the ```STATICFILES_STORAGE``` line.

After this we should be able to view our angular app's ```index.html``` when we run ```ng build --watch``` and ```python manage.py runserver```.

[Next](https://raw.githubusercontent.com/wgoode3/djangular/master/page4.md)