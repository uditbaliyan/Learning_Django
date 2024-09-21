

## [Setting up a Django Project](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#setting-up-a-django-project)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#setting-up-a-django-project)

Let’s set up our test Django project. First, create a folder called `projects` which is where our app will live.

```
mkdir projects && cd projects
```


Inside `projects`, let’s use `virtualenv` to create an environment for our app’s dependencies.

```
virtualenv env --python python3
```


NOTE: If you do not have `virtualenv` installed, install it using the command `pip install virtualenv`.

Once that is done, activate the environment by running the activate shell script.

```
source env/bin/activate
```


If that command works, you should see an `(env)` prompt on your terminal.

```
#(env)~/projects
$
```


Everything look fine? Awesome! Let’s now use `pip` to install `Django` into our environment.

```
#(env)~/projects
$ pip install django
```


That command should install Django into your environment. As of the time of writing, the Django version is `1.10.4`.

We are then going to call the `django-admin` script to create our Django app. Let’s do that like this:

```
#(env)~/projects
$ django-admin startproject djangotemplates
```


If you check your `projects` folder structure, you should now have a new folder called `djangotemplates` created by Django in addition to the earlier `env` folder we created.

`cd` into `djangotemplates`.

Your folder structure should now be similar to this:

```
djangotemplates
--djangotemplates
----**init**.py
----settings.py
----urls.py
----wsgi.py
--manage.py
```



## [Settings for managing static files](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#settings-for-managing-static-files)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#settings-for-managing-static-files)

Static files include stuff like CSS, JavaScript and images that you may want to serve alongside your site. Django is very opinionated about how you should include your static files. In this article, I will show how to go about adding static files to a Django application.

Open the `settings.py` file inside the inner `djangotemplates` folder. At the very bottom of the file you should see these lines:

```
# djangotemplates/djangotemplates/settings.py

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.10/howto/static-files/

STATIC_URL = '/static/'
```


This line tells Django to append static to the base url (in our case `localhost:8000`) when searching for static files. In Django, you could have a `static` folder almost anywhere you want. You can even have more than one `static` folder e.g. one in each app. However, to keep things simple, I will use just one `static` folder in the root of our project folder. We will create one later. For now, let’s add some lines in the `settings.py` file so that it looks like this.

```
# djangotemplates/djangotemplates/settings.py

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.10/howto/static-files/

STATIC_URL = '/static/'

# Add these new lines
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
)

STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```


The `STATICFILES_DIRS` tuple tells Django where to look for static files that are not tied to a particular app. In this case, we just told Django to also look for static files in a folder called `static` in our root folder, not just in our apps.

Django also provides a mechanism for collecting static files into one place so that they can be served easily. Using the `collectstatic` command, Django looks for all static files in your apps and collects them wherever you told it to, i.e. the `STATIC_ROOT`. In our case, we are telling Django that when we run `python manage.py collectstatic`, gather all static files into a folder called `staticfiles` in our project root directory. This feature is very handy for serving static files, especially in production settings.

## [App setup](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#app-setup)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#app-setup)

Create a folder called `static` on the same level as the inner `djangotemplates` folder and the `manage.py` file. You should now have this structure:

```
djangotemplates
--djangotemplates
----**init**.py
----settings.py
----urls.py
----wsgi.py
--static
--manage.py
```



Inside this folder is where we will have any custom CSS and JS we choose to write. On that note, let’s add two folders inside the static folder to hold our files, one called `css` and the other called `js`. Inside `css`, create a file called `main.css`. Add a `main.js` in the `js` folder as well. Your static folder should now look like this:

```
--static
----css
------main.cs
----js
------main.js
```


Once that is done, let’s create a new Django app called `example` that we will be working with. Do you remember how to do that? Don’t worry, it’s quite simple.

```
#(env)~/projects/djangotemplates
$ python manage.py startapp example
```


Once that is done, you should have a folder called `example` alongside `djangotemplates` and `static`. And of course you should still be able to see the `manage.py` file.

```
djangotemplates
--djangotemplates
----**init**.py
----settings.py
----urls.py
----wsgi.py
--example
--static
--manage.py
```


We need to tell Django about our new app. Go to the inner `djangotemplates` folder, open up `settings.py` and look for `INSTALLED_APPS`. Add `example` under the other included apps.

```
# djangotemplates/djangotemplates/settings.py

DEBUG = True

ALLOWED_HOSTS = []


# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'example', # Add this line
]
```

Just to recap, we now have the following folder structure:

```
djangotemplates
--djangotemplates
----**init**.py
----settings.py
----urls.py
----wsgi.py
--example
----migrations
------**init**.py
----admin.py
----apps.py
----models.py
----tests.py
----views.py
--static
----css
------main.cs
----js
------main.js
--manage.py
```


## [URL definition](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#url-definition)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#url-definition)

Let’s define a URL to go to our new app. Let’s edit `djangotemplates/djangotemplates/urls.py` to effect that.

```
# djangotemplates/djangotemplates/urls.py

from django.conf.urls import url, include # Add include to the imports here
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^', include('example.urls')) # tell django to read urls.py in example app
]
```


After that, in the `example` app folder, create a new file called `urls.py` and add the following code:

```
# djangotemplates/example/urls.py

from django.conf.urls import url
from example import views

urlpatterns = [
    path('', views.HomePageView.as_view(), name='home'), # Notice the URL has been named
    path('about/', views.AboutPageView.as_view(), name='about'),
]
```



The code we have just written tells Django to match the empty route (i.e localhost:8000) to a view called `HomePageView` and the route `/about/` to a view called `AboutPageView`. Remember, Django views take in HTTP requests and return HTTP responses. In our case, we shall use a `TemplateView` that returns a Home Page template and another one for the About page. To do this, inside your `example` app folder, create another folder called `templates`. Inside the new `templates` folder, create two new files called `index.html` and `about.html`. Your `example` app folder should now have this structure:

```
--example
----migrations
------**init**.py
----templates
------index.html
------about.html
----admin.py
----apps.py
----models.py
----tests.py
----urls.py
----views.py
```


Inside the `index.html`, paste the following code:

```
<!-- djangotemplates/example/templates/index.html-->

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Welcome Home</title>
</head>
<body>
  <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
    Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
    Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
    Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
  </p>
  <a href="{% url 'home' %}">Go Home</a>
  <a href="{% url 'about' %}">About This Site</a>
</body>
</html>
```


Add this code to `about.html`:

```
<!-- djangotemplates/example/templates/about.html-->

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>About Us</title>
</head>
<body>
  <p>
  We are a group of Django enthusiasts with the following idiosyncrasies:

  <ol>
    <li>We only eat bananas on Saturdays.</li>
    <li>We love making playing football on rainy days.</li>
  </ol>
  </p>
  <a href="{% url 'home' %}">Go Home</a>
  <a href="{% url 'about' %}">About This Site</a>
</body>
</html>
```


Notice how we are referring to our links for `Go Home` and `About This Site` in our templates. We can use Django’s automatic URL reverse lookup because we named our URLs in our `urls.py`. Neat, huh!

We shall see the effect of this code in the next section.

## [Wiring up the views](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#wiring-up-the-views)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#wiring-up-the-views)

Let’s add the final code to serve up our templates. We need to edit `djangotemplates/example/views.py` for this.

```
# djangotemplates/example/views.py
from django.shortcuts import render
from django.views.generic import TemplateView # Import TemplateView

# Add the two views we have been talking about  all this time :)
class HomePageView(TemplateView):
    template_name = "index.html"


class AboutPageView(TemplateView):
    template_name = "about.html"
```

Now we can run our app. We first need to make Django’s default migrations since this is the first time we are running our app.

```
#(env)~/projects/djangotemplates
$ python manage.py migrate
```

Once that is done, start your server.

```
#(env)~/projects/djangotemplates
$ python manage.py runserver
```


Open your browser and navigate to `http://localhost:8000`. You should be able to see our home page.

Clicking the links at the bottom should be able to navigate you between the pages. Here is the About page:

## [Template Inheritance](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#template-inheritance)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#template-inheritance)

Let’s shift our focus to the templates folder inside the `example` app folder. At the moment, it contains two templates, `index.html` and `about.html`.

We would like both these templates to have some CSS included. Instead of rewriting the same code in both of them, Django allows us to create a base template which they will both inherit from. This prevents us from having to write a lot of repeated code in our templates when we need to modify anything that is shared.

Let’s create the base template now. Create a file called `base.html` in `djangotemplates/example/templates`. Write this code inside it:

```
<!-- djangotemplates/example/templates/base.html -->

{% load static %}
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>
      Django Sample Site - {% block title %}{% endblock %}
    </title>

    <script src="{% static 'js/main.js' %}"></script> <!-- This is how to include a static file -->
    <link rel="stylesheet" href="{% static 'css/main.css' %}" type="text/css" />
  </head>
  <body>
    <div class="container">
      {% block pagecontent %}
      {% endblock %}
    </div>
  </body>
</html>
```

Copy

The very first line in the file, `{% load static %}`, uses Django’s special template tag syntax to tell the template engine to use the files in the `static` folder in this template.

In the title tag, we use a Django block. What this means is that in any Django template which inherits from this base template, any HTML which is inside a block named `title` will be plugged into the title block. The same goes for the body tag’s `pagecontent` block. If this sounds confusing, don’t worry. You will see it in action soon.

If you are not running your Django server, run it by executing `python manage.py runserver` in your terminal. Go to [http://localhost:8000](http://localhost:8000/). You should see the previous template.

Now edit the `index.html` template to inherit from the base template.

```
<!-- djangotemplates/example/templates/index.html -->

{% extends 'base.html' %} <!-- Add this for inheritance -->

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Welcome Home</title>
</head>
<body>
    <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
      Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
      Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
      Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
    </p>
    <a href="{% url 'home' %}">Go Home</a>
    <a href="{% url 'about' %}">About This Site</a>
</body>
</html>
```


Reload the page in your browser. Nothing appears! This is because Django expects your content to be written inside the blocks we defined in the base template so that they can be rendered. Edit the `index.html` to add the blocks:

```
<!-- djangotemplates/example/templates/index.html -->

{% extends 'base.html' %}

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{% block title %}Welcome Home {% endblock %}</title>
</head>
<body>
  {% block pagecontent %}
    <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
      Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
      Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
      Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
    </p>
    <a href="{% url 'home' %}">Go Home</a>
    <a href="{% url 'about' %}">About This Site</a>
  {% endblock %}
</body>
</html>
```



Reload the page in the browser and voila! Your content should appear again!

We can also edit the `about.html` template to use the same.

```
<!-- djangotemplates/example/templates/about.html -->

{% extends 'base.html' %} <!-- Add this for inheritance -->

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}About Us {% endblock %}</title>
</head>
<body>
  {% block pagecontent %}
    <p>
    We are a group of Django enthusiasts with the following idiosyncrasies:

    <ol>
        <li>We only eat bananas on Saturdays.</li>
        <li>We love making playing football on rainy days.</li>
    </ol>
    </p>
    <a href="{% url 'home' %}">Go Home</a>
    <a href="{% url 'about' %}">About This Site</a>
  {% endblock %}
</body>
</html>
```


Which is exactly the same as before!

However, now since both templates inherit from a base template, I can easily style them. Open up `main.css` in your `css` folder and add these styles:

```
.container {
    background: #eac656;
    margin: 10 10 10 10;
    border: 3px solid black;
}
```


This will style the container div which we are loading our content into. Refresh your browser. You should see this:


## [Rendering templates with data from views](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#rendering-templates-with-data-from-views)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#rendering-templates-with-data-from-views)

You can use Django’s template engine to display data in very powerful ways. In this section, I will create a Django view that will pass data into a template. I will then show you how to access that data in the template and display it to the user.

First things first, open up `views.py` in the `example` app folder. We will add a new view to serve data into our yet to exist `data.html` template. Modify the `views.py` file to look like this:

```
# djangotemplates/example/views.py

from django.shortcuts import render
from django.views.generic import TemplateView

class HomePageView(TemplateView):
    template_name = "index.html"

class AboutPageView(TemplateView):
    template_name = "about.html"

# Add this view
class DataPageView(TemplateView):
    def get(self, request, **kwargs):
        # we will pass this context object into the
        # template so that we can access the data
        # list in the template
        context = {
            'data': [
                {
                    'name': 'Celeb 1',
                    'worth': '3567892'
                },
                {
                    'name': 'Celeb 2',
                    'worth': '23000000'
                },
                {
                    'name': 'Celeb 3',
                    'worth': '1000007'
                },
                {
                    'name': 'Celeb 4',
                    'worth': '456789'
                },
                {
                    'name': 'Celeb 5',
                    'worth': '7890000'
                },
                {
                    'name': 'Celeb 6',
                    'worth': '12000456'
                },
                {
                    'name': 'Celeb 7',
                    'worth': '896000'
                },
                {
                    'name': 'Celeb 8',
                    'worth': '670000'
                }
            ]
        }

        return render(request, 'data.html', context)
```



We are using the same kind of view we used to render the other templates. However, we are now passing a `context` object to the render method. The key-value pairs defined in the context will be available in the template being rendered and we can iterate through them just like any other list.

To finish this up, go to the `urls.py` file in the `howdy` app and add the URL pattern for our new view so that it looks like this:

```
# djangotemplates/example/urls.py

from django.conf.urls import url
from example import views

urlpatterns = [
    url(r'^$', views.HomePageView.as_view(), name='home'),
    url(r'^about/$', views.AboutPageView.as_view(), name='about'),
    url(r'^data/$', views.DataPageView.as_view(), name='data'),  # Add this URL pattern
]
```


Finally, let’s create the template. In the `templates` folder, create a file called `data.html` and write this code inside it.

```
<!-- djangotemplates/example/templates/data.html -->

{% extends 'base.html' %}
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    {% block pagecontent %}
    <div class="table-div">
    <!-- We will display our data in a normal HTML table using Django's
    template for-loop to generate our table rows for us-->
      <table class="table">
        <thead>
          <tr>
            <th>Celebrity Name</th>
            <th>Net Worth</th>
          </tr>
        </thead>
        <tbody>
          {% for celebrity in data %}
            <tr>
              <td>{{ celebrity.name }}</td>
              <td>{{ celebrity.worth }}</td>
            </tr>
          {% endfor %}
        </tbody>
      </table>
    </div>
    {% endblock %}
  </body>
</html>
```


In `data.html`, you can see that we use what is essentially a for loop to go through the data list. Binding of values in Django templates is done using `{{}}` curly brackets much like in AngularJS.

With your server running, go to `http://localhost:8000/data/` to see the template.

## [Including snippets into your templates](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#including-snippets-into-your-templates)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#including-snippets-into-your-templates)

We now have three templates, `index.html`, `about.html` and `data.html`. Let’s link them together using a simple navigation bar. First up, let’s write the code for the navigation bar in another HTML template.

In the templates folder inside the `example` app, create a new folder called `partials`. Inside it, create a file called `nav-bar.html`. The templates folder structure should now be like this:

```
templates
----index.html
----about.html
----data.html
----partials
------nav-bar.html
```



Edit the `nav-bar.html` partial so that it contains this code:

```
<!-- djangotemplates/example/templates/partials/nav-bar.html -->

<div class="nav">
  <a href="{% url 'home' %}">Go Home</a>
  <a href="{% url 'about' %}">About This Site</a>
  <a href="{% url 'data' %}">View Data</a>
</div>
```

Including snippets in a template is very simple. We use the `includes` keyword provided by Django’s templating engine. Go ahead and modify `index.html` to this:

```
<!-- djangotemplates/example/templates/index.html -->

{% extends 'base.html' %}

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>{% block title %}Welcome Home {% endblock %}</title>
</head>
<body>
  {% block pagecontent %}
    <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
      Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. 
      Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. 
      Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
    </p>
    {% include 'partials/nav-bar.html' %} <!--Add this-->

    <!-- Remove these two lines -- >
    <!-- <a href="{% url 'home' %}">Go Home</a> -->
    <!-- <a href="{% url 'about' %}">About This Site</a> -->
  {% endblock %}
</body>
</html>
```



Modify `about.html` to this:

```
<!-- djangotemplates/example/templates/about.html -->

{% extends 'base.html' %}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}About Us {% endblock %}</title>
</head>
<body>
  {% block pagecontent %}
    <p>
    We are a group of Django enthusiasts with the following idiosyncrasies:

    <ol>
        <li>We only eat bananas on Saturdays.</li>
        <li>We love making playing football on rainy days.</li>
    </ol>
    </p>
    {% include 'partials/nav-bar.html' %} <!--Add this-->

    <!-- Remove these two lines -- >
    <!-- <a href="{% url 'home' %}">Go Home</a> -->
    <!-- <a href="{% url 'about' %}">About This Site</a> -->
  {% endblock %}
</body>
</html>
```


Lastly, modify `data.html` to this:

```
<!-- djangotemplates/example/templates/data.html -->

{% extends 'base.html' %}
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    {% block pagecontent %}
    <div class="table-div">
      <table class="table">
        <thead>
          <tr>
            <th>Celebrity Name</th>
            <th>Net Worth</th>
          </tr>
        </thead>
        <tbody>
          {% for celebrity in data %}
            <tr>
              <td>{{ celebrity.name }}</td>
              <td>{{ celebrity.worth }}</td>
            </tr>
          {% endfor %}
        </tbody>
      </table>
    </div>
    {% include 'partials/nav-bar.html' %} <!--Add this-->
    {% endblock %}
  </body>
</html>
```



Time to check out our work! Open your browser and navigate to `http://localhost:8000`. You should see this:

All the pages are now linked with the navbar so you can easily navigate back and forth through them, all with minimal code written. Here is the `data.html` template:

And here is `about.html`:

Note: I have added the following CSS to syle the links in the navbar. Feel free to use it or play with your own styles:

```
// djangtotemplates/static/css/main.css

.container {
    background: #eac656;
    margin: 10 10 10 10;
    border: 3px solid black;
}

.nav a {
    background: #dedede;
}
```



## [Filters](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#filters)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#filters)

Filters take data piped to them and output it in a formatted way. Django templates have access to the `humanize` collection of filters, which make data more human readable. Let’s make the celebrity’s networth field in the data template more readable by using some of these filters.

To use Django’s humanize filters, you first need to edit some settings. Open up `djangotemplates/settings.py` and edit the `INSTALLED_APPS` list to this:

```
# djangotemplates/djangotemplates/settings.py

ALLOWED_HOSTS = []


# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.contrib.humanize', # Add this line. Don't forget the trailing comma
    'example',
]
```

Copy

We can now use a filter in our templates. We are going to use the `intcomma` filter to add comma’s in large numbers to make them easier to read. Let’s modify `data.html` to this:

```
<!-- djangotemplates/example/templates/data.html -->

{% extends 'base.html' %}
{% load humanize %} <!-- Add this-->

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title></title>
  </head>
  <body>
    {% block pagecontent %}
    <div class="table-div">
      <table class="table">
        <thead>
          <tr>
            <th>Celebrity Name</th>
            <th>Net Worth</th>
          </tr>
        </thead>
        <tbody>
          {% for celebrity in data %}
            <tr>
              <td>{{ celebrity.name }}</td>
              <td>$ {{ celebrity.worth | intcomma }}</td> <!--Modify this line-->
            </tr>
          {% endfor %}
        </tbody>
      </table>
    </div>
    {% include 'partials/nav-bar.html' %}
    {% endblock %}
  </body>
</html>
```

Copy

When you go to `http://localhost:8000/data/`, you should now have a more friendly list of net worth values:

There are many more filters included in the `humanize` package. Read about them [here](https://docs.djangoproject.com/en/1.10/ref/contrib/humanize/)

## [Collecting Static Files](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#collecting-static-files)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#collecting-static-files)

Remember we talked about collecting static files? Try the following command:

```
python manage.py collectstatic
```

Copy

You should see a prompt like the following:

```
You have requested to collect static files at the destination
location as specified in your settings:

      /Users/amos/projects/djangotemplates/staticfiles

This will overwrite existing files!
Are you sure you want to do this?

Type 'yes' to continue, or 'no' to cancel:
```


Go ahead and say `yes`.

This command will tell Django to go through all your project folders, look for all static files and store them in one place (the static root we defined in the settings). This is very efficient especially if you are deploying your site to production.

When you run the command `collectstatic`, you should see a new folder called `staticfiles` created in the root of your project folder. You can change this location to something else by editing the static root setting in your project’s `settings.py` file. To use these `staticfiles`, in your templates you will say `load staticfiles` instead of `load static`. Everything else is the same as with using the previous `static` folder.

## [Conclusion](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#conclusion)[](https://www.digitalocean.com/community/tutorials/working-with-django-templates-static-files#conclusion)

Congratulations on reaching the end of this tutorial! By now you should have a more detailed understanding of how Django templates work. If you need deeper information, remember the docs are your friend. You can find the full code for this tutorial [here](https://github.com/andela-aomondi/djangotemplates). Make sure to leave any thoughts, questions or concerns in the comments below.

Thanks for learning with the DigitalOcean Community. Check out our offerings for compute, storage, networking, and managed databases.

[Learn more about us](https://www.digitalocean.com/)


```
# for the "Settings for managing static files" section
# best to not import new stuff, use django 4's standard of using pathlib Path
STATIC_ROOT  = Path.joinpath(BASE_DIR, 'staticfiles')
STATIC_URL = '/static/'
STATICFILES_DIRS = [Path.joinpath(BASE_DIR, 'static'), ]
```

Also a question, why do we create STATIC_ROOT with “staticfiles” and not “static”? I understand that `collectstatic` will put all static files into the specified directory. Wouldn’t “static” be better?

Why is “staticfiles” not declared in the STATICFILES_DIRS list if there is potentially going to be static files there?



I am making website like convert any file to encrypted file . So how should the code be if user uploads the file and clicks on encrypt button and goes to download.html template and by clicking on download button the users get the file downloaded. I searched each and every approach but there is some or other mistake. So kindly Help me regarding And also many others like me who are struggling with the same. Thank you.



I am making website like convert any file to encrypted file . So how should the code be if user uploads the file and clicks on encrypt button and goes to download.html template and by clicking on download button the users get the file downloaded. I searched each and every approach but there is some or other mistake. So kindly Help me regarding And also many others like me who are struggling with the same. Thank you.



Great, Quick review, but we nned to have different static names for development and production or just keep it as load static always…

Thanks



Thanks for the article!

You wrote “To use these staticfiles, in your templates you will say load staticfiles instead of load static. Everything else is the same as with using the previous static folder.”

After some investigation, it seems this has been deprecated since Django V1.10, around 2016. If anybody notices this “load staticfiles”, it’s not required now.



I’ve created a Data model:

from django.db import models

class Data(models.Model): name = models.CharField(‘Name’, max_length=100) worth = models.IntegerField(‘Worth’, max_length=20)

```
def __str__(self):
	return self.name
```

And then I changed the DataViewPage view:

class DataPageView(ListView): model = Data template_name = ‘data.html’

And then I changed also the data.html file:

{% for celebrity in object_list %} <tr> <td>{{ [celebrity.name](http://celebrity.name/) }}</td> <td>$ {{ celebrity.worth | intcomma }}</td> </tr> {% endfor %}

And after register the model in [admin.py](http://admin.py/) and doing makemigratios and migrate I could enter all that Celeb data via the admin page.


![close](https://www.digitalocean.com/_next/static/media/close-x.5381fe8a.svg)
