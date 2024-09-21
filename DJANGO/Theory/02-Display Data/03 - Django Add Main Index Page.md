___

## Main Index Page

Our project needs a main page.

The main page will be the landing page when someone visits the root folder of the project.

Now, you get an error when visiting the root folder of your project:

`[127.0.0.1:8000/](http://127.0.0.1:8000/)`.

Start by creating a template called `main.html`:

### Main[Get your own Django Server](https://www.w3schools.com/django/django_server.php "W3Schools Spaces")

`my_tennis_club/members/templates/main.html`:

```django
{% extends "master.html" %} 
{% block title %} My Tennis Club {% endblock %}
{% block content %} 
<h1>My Tennis Club</h1>
<h3>Members</h3>
<p>Check out all our <a href="members/">members</a></p>
{% endblock %}
```

___

## Create new View

Then create a new view called `main`, that will deal with incoming requests to root of the project:

`my_tennis_club/members/views.py`:

```jsx
from django.http import HttpResponse
from django.template import loader
from .models import Member 

def members(request):
	mymembers = Member.objects.all().values()
	template = loader.get_template('all_members.html')
	context = { 'mymembers': mymembers, } 
	return HttpResponse(template.render(context, request))
	
def details(request, id):
	mymember = Member.objects.get(id=id)
	template = loader.get_template('details.html')
	context = { 'mymember': mymember, } 
	return HttpResponse(template.render(context, request))
	
def main(request):
	template = loader.get_template('main.html') 
	return HttpResponse(template.render())
```

The `main` view does the following:

-   loads the `main.html` template.
-   Outputs the HTML that is rendered by the template.

___

## Add URL

Now we need to make sure that the root url points to the correct view.

Open the `urls.py` file and add the main view to the `urlpatterns` list:

`my_tennis_club/members/urls.py`:

```jsx
from django.urls import path
from . import views 
urlpatterns = [ 
path('', views.main, name='main'),
path('members/', views.members, name='members'), path('members/details/<int:id>', views.details, name='details'), ]
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_add_main)

___

## Add Link Back to Main

The members page is missing a link back to the main page, so let us add that in the `all_members.html` template, in the `content` block:

### Example

`my_tennis_club/members/templates/all_members.html`:

```django
{% extends "master.html" %} 
{% block title %} My Tennis Club - List of all members {% endblock %}
{% block content %} 
<p><a href="/">HOME</a></p> 
<h1>Members</h1>
<ul> {% for x in mymembers %}
<li><a href="details/{{ x.id }}">{{ x.firstname }} {{ x.lastname }}</a></li> 
{% endfor %} 
</ul> 
{% endblock %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_link_to_home)

If you have followed all the steps on your own computer, you can see the result in your own browser: `[127.0.0.1:8000/](http://127.0.0.1:8000/)`.

If the server is down, you have to start it again with the `runserver` command:

___

W3schools Pathfinder

Track your progress - it's free!