___

## Get Data

There are different methods to get data from a model into a QuerySet.

___

## The values() Method

The `values()` method allows you to return each object as a Python dictionary, with the names and values as key/value pairs:

### Example[Get your own Django Server](https://www.w3schools.com/django/django_server.php "W3Schools Spaces")

`views.py`:

```jsx
from django.http import HttpResponse from django.template import loader from .models import Member def testing(request): mydata = Member.objects.all().values() template = loader.get_template('template.html') context = { 'mymembers': mydata, } return HttpResponse(template.render(context, request))
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_queryset_get)

___

## Return Specific Columns

The `values_list()` method allows you to return only the columns that you specify.

### Example

Return only the `firstname` columns:

`views.py`:

```jsx
from django.http import HttpResponse from django.template import loader from .models import Member def testing(request): mydata = Member.objects.values_list('firstname') template = loader.get_template('template.html') context = { 'mymembers': mydata, } return HttpResponse(template.render(context, request))
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_queryset_get2)

___

## Return Specific Rows

You can filter the search to only return specific rows/records, by using the `filter()` method.

### Example

Return only the records where `firstname` is 'Emil'

`views.py`:

```jsx
from django.http import HttpResponse from django.template import loader from .models import Member def testing(request): mydata = Member.objects.filter(firstname='Emil').values() template = loader.get_template('template.html') context = { 'mymembers': mydata, } return HttpResponse(template.render(context, request))
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_queryset_get3)

You will learn more about the `filter()` method in the [next chapter](https://www.w3schools.com/django/django_queryset_filter.php).

___

W3schools Pathfinder

Track your progress - it's free!