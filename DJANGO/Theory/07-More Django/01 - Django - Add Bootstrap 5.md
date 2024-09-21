## Django - Add Static File

___

There are two main methods to use bootstrap in your Django project. Either by downloading the required files and include them in your project, or you can install the bootstrap 5 module in your [virtual environment](https://www.w3schools.com/django/django_create_virtual_environment.php).

We will use the second method, installing Bootstrap 5 in the virtual environment.

___

## Install Bootstrap 5

Bootstrap 5 should be installed in the virtual environment.

We will install it in an existing project, the [My Tennis Club project](https://www.w3schools.com/django/django_create_project.php), created earlier in this tutorial.

Open the command view, navigate to the virtual environment folder and activate the virtual environment:

Once you are inside the virtual environment, install Bootstrap 5 with this command:

pip install django-bootstrap-v5

Which will give you a result like this:

Collecting django-bootstrap-v5  
Downloading django\_bootstrap\_v5-1.0.11-py3-none-any.whl (24 kB)  
Requirement already satisfied: django<5.0,>=2.2 in c:\\users\\_your name_\\myworld\\lib\\site-packages (from django-bootstrap-v5) (4.1.4)  
Collecting beautifulsoup4<5.0.0,>=4.8.0  
  Downloading beautifulsoup4-4.11.1-py3-none-any.whl (128 kB)  
     |████████████████████████████████| 128 kB 6.4 MB/s  
Requirement already satisfied: tzdata; sys\_platform == "win32" in c:\\users\\_your name_\\myworld\\lib\\site-packages (from django<5.0,>=2.2->django-bootstrap-v5) (2022.7)  
Requirement already satisfied: asgiref<4,>=3.5.2 in c:\\users\\_your name_\\myworld\\lib\\site-packages (from django<5.0,>=2.2->django-bootstrap-v5) (3.5.2)  
Requirement already satisfied: sqlparse>=0.2.2 in c:\\users\\_your name_\\myworld\\lib\\site-packages (from django<5.0,>=2.2->django-bootstrap-v5) (0.4.3)  
Collecting soupsieve>1.2  
  Downloading soupsieve-2.3.2.post1-py3-none-any.whl (37 kB)  
Installing collected packages: soupsieve, beautifulsoup4, django-bootstrap-v5  
Successfully installed beautifulsoup4-4.11.1 django-bootstrap-v5-1.0.11 soupsieve-2.3.2.post1

___

## Update Settings

Next step is to include the bootstrap module in the `INSTALLED_APPS` list in `settings.py`:

`my_tennis_club/my_tennis_club/settings.py`:

```jsx
INSTALLED_APPS = [ 'django.contrib.admin', 'django.contrib.auth', 'django.contrib.contenttypes', 'django.contrib.sessions', 'django.contrib.messages', 'django.contrib.staticfiles', 'members', 'bootstrap5', ]
```

Bootstrap 5 is now ready to use in your project!

___

## Remove Old Styling

ThThe My Tennis Club project already has a stylesheet, remove it and the Members page without styling will look like this:

![](https://www.w3schools.com/django/screenshot_django_members1.png)

___

## Add Bootstrap 5 to Template

To use Bootstrap 5 in the project, start by inserting some lines of code in the `master.html` template:

`my_tennis_club/members/templates/master.html`:

```django
<!DOCTYPE html> <html> <head> <title>{% block title %}{% endblock %}</title> {% load bootstrap5 %} {% bootstrap_css %} {% bootstrap_javascript %} </head> <body> <div class="container"> <ul class="nav bg-info"> <li class="nav-item"> <a class="nav-link link-light" href="/">HOME</a> </li> <li class="nav-item"> <a class="nav-link link-light" href="/members">MEMBERS</a> </li> </ul> {% block content %} {% endblock %} </div> </body> </html>
```

As you can see, we inserted these three lines in the `<head>` section:

```django
{% load bootstrap5 %} {% bootstrap_css %} {% bootstrap_javascript %}
```

The first line tells Django that it should load the Bootstrap 5 module in this template.

The second line inserts the `<link>` element with the referral to the bootstrap stylesheet.

The third line inserts the `<script>` element with the referral to the necessary javascript file.

We also did some changes to the HTML elements in the template, like inserting bootstrap classes to the navigation bar:

```django
<div class="container"> <ul class="nav bg-info"> <li class="nav-item"> <a class="nav-link link-light" href="/">HOME</a> </li> <li class="nav-item"> <a class="nav-link link-light" href="/members">MEMBERS</a> </li> </ul> {% block content %} {% endblock %} </div>
```

If you run the project now, the members page will look like this:

![](https://www.w3schools.com/django/screenshot_django_bs51.png)

That's it! Bootstrap 5 is now a part of your project!

Learn more about Bootstrap 5 in our [Bootstrap 5 Tutorial](https://www.w3schools.com/bootstrap5/index.php).

___

W3schools Pathfinder

Track your progress - it's free!

   [![Get Certified](https://www.w3schools.com/images/img_fullaccess_up_sep1_green_300.png)](https://campus.w3schools.com/products/w3schools-full-access-course)