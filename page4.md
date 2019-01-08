# Getting and Posting data to our Django server

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

<hr>

### Where is the data in request.POST?

```python

class Papayas(View):

    def post(self, request):
    	print(request.POST)
        return JsonResponse({'status': 'ok'})
```

When we attempt to print the dictionary of form data after posting to our backend server, we may imagine that the data will still be there in ```request.POST``` like it is when we used Django before. Now that the data is being sent back as JSON by angular, we have to look instead in ```request.body```


```python

class Papayas(View):

    def post(self, request):
    	print(request.body)
        return JsonResponse({'status': 'ok'})
```

We are likely to get back something that looks like the following however... ```b'{"name": "Pappy", "is_ripe": true}'```. This is coming back to us as a bytestring, so the first thing we will need to do is ```.decode()``` this into a ```utf-8``` encoded string. Next if we want to take this string and convert it into an easier to work with dictionary, we can do so using the ```json``` library.

```python

# add this import
import json

class Papayas(View):

    def post(self, request):
    	our_data = json.loads(request.body.decode())
	print(our_data, type(our_data)
        return JsonResponse({'status': 'ok'})
```

Our data should now be a dictionary that we can use however we want to.

<hr>

### How do we respond back with data from our database?

We might naively consider trying something like this...

```python
# add this import
from .models import Papaya

class Papayas(View):

    def get(self, request):
        return JsonResponse({'status': 'ok', 'papayas': Papaya.objects.all()})
```

However when we do so we are likely to see an error, specifically ```Object of type QuerySet is not JSON Serializable```. 

We can get around this particular error by converting the QuerySet (a Django object that is essentially a list of objects from out models) into a list.

```python
# instead of
Papaya.objects.all()
# use
list(Papaya.objects.all())
```

When what is being returned by the Django ORM is a QuerySet (ie when we use ```.all()``` or ```.filter()```) we will have to do this conversion.

After making this change though we are still not done. The QuerySet has been changed to a list that is JSON Serialiazable (can be converted into a JSON Object to send as a JsonResponse) however it contains instances of the Papaya class from our models that also are not JSON Serializable. So we will have to alter what we're doing just a little bit more and make use of the ```.values()``` method.

```python
# instead of
list(Papaya.objects.all())
# use
list(Papaya.objects.values().all())
```

This will return just the values (a dictionary) of each entry in our database instead of an instance of the ```Papaya``` class. 

[Next](https://github.com/wgoode3/djangular/blob/master/page5.md)
