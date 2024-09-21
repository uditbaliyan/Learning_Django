___

## Templates

In the [Django Intro](https://www.w3schools.com/django/django_intro.php) page, we learned that the result should be in HTML, and it should be created in a template, so let's do that.

Create a `templates` folder inside the `members` folder, and create a HTML file named `myfirst.html`.

The file structure should be like this:

```
my\_tennis\_club  
    manage.py  
    my\_tennis\_club/  
    members/  
        templates/  
            myfirst.html  
```
Open the HTML file and insert the following:

`my_tennis_club/members/templates/myfirst.html`:

```html
<!DOCTYPE html> 
<html> 
	<body> 
		<h1>Hello World!</h1> 
		<p>Welcome to my first Django project!</p> 
	</body> 
</html>
```

___

## Modify the View

Open the `views.py` file and replace the `members` view with this:

`my_tennis_club/members/views.py`:

```python
from django.http import HttpResponse 
from django.template import loader 
def members(request): 
	template = loader.get_template('myfirst.html') 
	return HttpResponse(template.render())
```

___

## Change Settings

To be able to work with more complicated stuff than "Hello World!", We have to tell Django that a new app is created.

This is done in the `settings.py` file in the `my_tennis_club` folder.

Look up the `INSTALLED_APPS[]` list and add the `members` app like this:

`my_tennis_club/my_tennis_club/settings.py`:

```python

INSTALLED_APPS = [ 
	'django.contrib.admin',
	'django.contrib.auth',
	'django.contrib.contenttypes',
	'django.contrib.sessions',
	'django.contrib.messages',
	'django.contrib.staticfiles',
	'members'
]
```



Start the server by navigating to the `/my_tennis_club` folder and execute this command:

In the browser window, type `[127.0.0.1:8000/members/](http://127.0.0.1:8000/members/)` in the address bar.

The result should look like this:

![](https://www.w3schools.com/django/screenshot_django_template_myfirst.png)

___

