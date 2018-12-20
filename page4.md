# Getting and Posting data to our Django server

### Contents:
* [Using Angular with Django](https://github.com/wgoode3/djangular/blob/master/page1.md)
* [Taking Django to the SPA](https://github.com/wgoode3/djangular/blob/master/page2.md)
* [Connecting Angular + Middleware Settings](https://github.com/wgoode3/djangular/blob/master/page3.md)
* Getting and Posting data to our Django server
* [Assignment 1 - Django Angular Tasks](https://github.com/wgoode3/djangular/blob/master/page5.md)
* [Using a database other than SQLite (Optional)](https://github.com/wgoode3/djangular/blob/master/page6.md)
* [Assignment 2 - Django Angular Login and Registration](https://github.com/wgoode3/djangular/blob/master/page7.md)
* [Assignment 3 - Django Angular E-Commerce (Highly Optional)](https://github.com/wgoode3/djangular/blob/master/page8.md)

<a href="https://youtu.be/OHww_idvEss" target="_blank">
	<img src="https://i.ytimg.com/vi/OHww_idvEss/hqdefault.jpg" alt="thumbnail">
</a>

In order to get and receive requests, we need to first configure our ```urls.py```.

```python
from django.urls import path
from papaya_app.views import Papayas, PapayaDetails

urlpatterns = [
    path('papaya', Papayas.as_view()),
    path('papaya/<int:papaya_id>', PapayaDetails.as_view())
]
```

#### Note: we have elected to use version 2+ for Django, for older versions you will need to use the url function instead of path

Next we will need to create the ```Papayas``` and ```PapayaDetails``` classes in our ```views.py```. To make setting up our Django server with RESTful routes easier we will be making use of Django's [class based views](https://docs.djangoproject.com/en/2.1/topics/class-based-views/). 

Inside of ```papaya_app/views.py``` we will need to add the following code.

```python
from django.http import JsonResponse
from django.views import View

class Papayas(View):

    def get(self, request):
        return JsonResponse({'status': 'ok'})

    def post(self, request):
        return JsonResponse({'status': 'ok'})

class PapayaDetails(View):

    def get(self, request, papaya_id):
        return JsonResponse({'status': 'ok'})

    def put(self, request, papaya_id):
        return JsonResponse({'status': 'ok'})

    def delete(self, request, papaya_id):
        return JsonResponse({'status': 'ok'})
```

Using class based views we can handle all 5 routes we need with only two classes.

| Verb   | Route     | Description                         |
|--------|-----------|-------------------------------------|
| GET    | /papaya   | Return a list of all of our papayas |
| POST   | /papaya   | Create a new papaya                 |
| GET    | /papaya/3 | Return the papaya with id = 3       |
| PUT    | /papaya/3 | Update the papaya with id = 3       |
| DELETE | /papaya/3 | Delete the papaya with id = 3       |

The next thing to notice is that we aren't using ```render``` or ```redirect```. Aside from serving the one static ```index.html``` page, we want this server to only respond with JSON, so every route receives a JsonResponse.

[Next](https://github.com/wgoode3/djangular/blob/master/page5.md)