___

## Handle Static Files

Static files in your project, like stylesheets, JavaScripts, and images, are not handled automatically by Django when `DEBUG = False`.

When `DEBUG = True`, this worked fine, all we had to do was to put them in the `static` folder of the application.

When `DEBUG = False`, static files have to be collected and put in a specified folder before we can use it.

___

## Collect Static Files

To collect all necessary static files for your project, start by specifying a `STATIC_ROOT` property in the `settings.py` file.

This specifies a folder where you want to collect your static files.

You can call the folder whatever you like, we will call it `productionfiles`:

`my_tennis_club/my_tennis_club/settings.py`:

```jsx
. . STATIC_ROOT = BASE_DIR / 'productionfiles' STATIC_URL = 'static/' . .
```

You could manually create this folder and collect and put all static files of your project into this folder, but Django has a command that do this for you:

py manage.py collectstatic

Which will produce this result:

131 static files copied to 'C:\\Users\\_your\_name_\\myworld\\my\_tennis\_club\\productionfiles'.

131 files? Why so many? Well this is because of the admin user interface, that comes built-in with Django. We want to keep this feature in production, and it comes with a whole bunch of files including stylesheets, fonts, images, and JavaScripts.

my\_tennis\_club  
    members/  
    my\_tennis\_club/  
    productionfiles/  
        admin/  
        myfirst.css  

___

## The Example Should Work

Now you have collected the static files of your project, and if you have [installed WhiteNoise](https://www.w3schools.com/django/django_static_whitenoise.php), the example from the [Add Static Files](https://www.w3schools.com/django/django_add_static_files.php) chapter will finally work.

Start the server and see the result:

And check out the result in your own browser: `[127.0.0.1:8000/testing/](http://127.0.0.1:8000/testing/)`.

### Example[Get your own Django Server](https://www.w3schools.com/django/django_server.php "W3Schools Spaces")

`my_tennis_club/members/templates/template.html`:

```django
{% load static %} <!DOCTYPE html> <html> <link rel="stylesheet" href="{% static 'myfirst.css' %}"> <body> {% for x in fruits %} <h1>{{ x }}</h1> {% endfor %} </body> </html>
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_static_css)

___

W3schools Pathfinder

Track your progress - it's free!

   [![Get Certified](https://www.w3schools.com/images/img_fullaccess_up_sep1_green_300.png)](https://campus.w3schools.com/products/w3schools-full-access-course)