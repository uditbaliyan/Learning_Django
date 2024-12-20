___

## Create Static Folder

When building web applications, you probably want to add some static files like images or css files.

Start by creating a folder named `static` in your project, the same place where you created the `templates` folder:

The name of the folder has to be `static`.

my\_tennis\_club  
    manage.py  
    my\_tennis\_club/  
    members/  
        templates/  
        static/  

Add a CSS file in the `static` folder, the name is your choice, we will call it `myfirst.css` in this example:

my\_tennis\_club  
    manage.py  
    my\_tennis\_club/  
    members/  
        templates/  
        static/  
            myfirst.css  

Open the CSS file and insert the following:

`my_tennis_club/members/static/myfirst.css`:

```css
body { background-color: lightblue; font-family: verdana; }
```

___

## Modify the Template

Now you have a CSS file, with some CSS styling. The next step will be to include this file in a HTML template:

Open the HTML file and add the following:

```django
{% load static %}
```

And:

```django
<link rel="stylesheet" href="{% static 'myfirst.css' %}">
```

### Example[Get your own Django Server](https://www.w3schools.com/django/django_server.php "W3Schools Spaces")

`my_tennis_club/members/templates/template.html`:

```django
{% load static %} <!DOCTYPE html> <html> <link rel="stylesheet" href="{% static 'myfirst.css' %}"> <body> {% for x in fruits %} <h1>{{ x }}</h1> {% endfor %} </body> </html>
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_static_css)

Restart the server for the changes to take effect:

And check out the result in your own browser: `[127.0.0.1:8000/testing/](http://127.0.0.1:8000/testing/)`.

## Didn't Work?

**Just testing?** If you just want to play around, and not going to deploy your work, you can set `DEBUG = True` in the `settings.py` file, and the example above will work.

**Plan to deploy?** If you plan to deploy your work, you should set `DEBUG = False` in the `settings.py` file. The example above will fail, because Django has no built-in solution for serving static files, but there are other ways to serve static files, you will learn how in the next chapter.

### Example (in development):

`my_tennis_club/my_tennis_club/settings.py`:

```jsx
. . # SECURITY WARNING: don't run with debug turned on in production! DEBUG = True . .
```

This will make the example work, but we want you to choose `DEBUG = False`, because that is the best way to learn how to work with Django.

___

## Choose Debug = False

For the rest of this tutorial, we will run with `DEBUG = False`, even in development, because that is the best way to learn how to work with Django.

### Example:

`my_tennis_club/my_tennis_club/settings.py`:

```jsx
. . # SECURITY WARNING: don't run with debug turned on in production! DEBUG = False ALLOWED_HOSTS = ['*'] . .
```

<big><code>ALLOWED_HOSTS</code></big>

When using `DEBUG = False` you have to specify which host name(s) are allowed to host your work. You could choose `'127.0.0.1'` or `'localhost'` which both represents the address of your local machine.

We choose `'*'`, which means _any_ address are allowed to host this site. This should be change into a real domain name when you deploy your project to a public server.

___

## Didn't Work?

That is right, the example _still_ does not work.

You will have install a third-party library in order to handle static files.

There are many alternatives, we will show you how to use a Python library called **WhiteNoise** in the [next chapter](https://www.w3schools.com/django/django_static_whitenoise.php).

___

W3schools Pathfinder

Track your progress - it's free!

   [![Get Certified](https://www.w3schools.com/images/img_fullaccess_up_sep1_green_300.png)](https://campus.w3schools.com/products/w3schools-full-access-course)