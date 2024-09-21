## Django - Installing WhiteNoise

___

Django does not have a built-in solution for serving static files, at least not in production when `DEBUG` has to be `False`.

We have to use a third-party solution to accomplish this.

In this Tutorial we will use WhiteNoise, which is a Python library, built for serving static files.

___

## Install WhiteNoise

To install WhiteNoise in your virtual environment, type the command below:

The result should be something like this:

Collecting whitenoise  
  Downloading whitenoise-6.2.0-py3-none-any.whl (19 kB)  
Installing collected packages: whitenoise  
Successfully installed whitenoise-6.2.0  
WARNING: You are using pip version 20.2.3; however, version 22.3.1 is available.  
You should consider upgrading via the 'c:\\users\\_Your Name_\\myworld\\scripts\\python.exe -m pip install --upgrade pip' command.

___

## Modify Settings

To make Django aware of you wanting to run WhitNoise, you have to specify it in the `MIDDLEWARE` list in `settings.py` file:

`my_tennis_club/my_tennis_club/settings.py`:

```jsx
. . MIDDLEWARE = [ 'django.middleware.security.SecurityMiddleware', 'django.contrib.sessions.middleware.SessionMiddleware', 'django.middleware.common.CommonMiddleware', 'django.middleware.csrf.CsrfViewMiddleware', 'django.contrib.auth.middleware.AuthenticationMiddleware', 'django.contrib.messages.middleware.MessageMiddleware', 'django.middleware.clickjacking.XFrameOptionsMiddleware', 'whitenoise.middleware.WhiteNoiseMiddleware', ]. .
```

___

## Collect Static Files

There are one more action you have to perform before you can serve the static file from the example in the [previous chapter](https://www.w3schools.com/django/django_add_static_files.php). You have to collect all static files and put them into one specified folder. You will learn how in the [next chapter](https://www.w3schools.com/django/django_collect_static_files.php).

___

W3schools Pathfinder

Track your progress - it's free!