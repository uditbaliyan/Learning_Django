___

## My First Project

Once you have come up with a suitable name for your Django project, like mine: `my_tennis_club`, navigate to where in the file system you want to store the code (in the virtual environment), I will navigate to the `myworld` folder, and run this command in the command prompt:
```

django-admin startproject my_tennis_club
```
Django creates a `my_tennis_club` folder on my computer, with this content:
```
my_tennis_club  
    manage.py  
    my_tennis_club/  
        __init__.py  
        asgi.py  
        settings.py  
        urls.py  
        wsgi.py  
```
These are all files and folders with a specific meaning, you will learn about some of them later in this tutorial, but for now, it is more important to know that this is the location of your project, and that you can start building applications in it.

___

## Run the Django Project

Now that you have a Django project, you can run it, and see what it looks like in a browser.

Navigate to the `/my_tennis_club` folder and execute this command in the command prompt:

Which will produce this result:

Watching for file changes with StatReloader  
Performing system checks...

System check identified no issues (0 silenced).

```You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.  
Run 'python manage.py migrate' to apply them.  
October 27, 2022 - 13:03:14  
Django version 4.1.2, using settings 'my\_tennis\_club.settings'  
Starting development server at http://127.0.0.1:8000/  
Quit the server with CTRL-BREAK.

Open a new browser window and type `[127.0.0.1:8000](http://127.0.0.1:8000/)` in the address bar.
```
The result:

![](https://www.w3schools.com/django/screenshot_django1.png)

___

## What's Next?

We have a Django project!

The next step is to make an app in your project.

You cannot have a web page created with Django without an app.

___
