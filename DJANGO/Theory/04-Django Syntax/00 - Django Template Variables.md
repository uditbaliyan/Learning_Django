___

## Template Variables

In Django templates, you can render variables by putting them inside `{{ }}` brackets:

___

## Create Variable in View

The variable `firstname` in the example above was sent to the template via a view:

`views.py`:

```jsx
from django.http import HttpResponse from django.template import loader def testing(request): template = loader.get_template('template.html') context = { 'firstname': 'Linus', } return HttpResponse(template.render(context, request))
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_variables2)

As you can see in the view above, we create an object named context and fill it with data, and send it as the first parameter in the `template.render()` function.

___

## Create Variables in Template

You can also create variables directly in the template, by using the `{% with %}` template tag.

The variable is available until the `{% endwith %}` tag appears:

### Example

`templates/template.html`:

```django
{% with firstname="Tobias" %} <h1>Hello {{ firstname }}, how are you?</h1> {% endwith %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_variables3)

You will learn more about [template tags](https://www.w3schools.com/django/django_template_tags.php) in the next chapter.

___

## Data From a Model

The example above showed a easy approach on how to create and use variables in a template.

Normally, most of the external data you want to use in a template, comes from a model.

We have created a model in the previous chapters, called `Member`, which we will use in many examples in the next chapters of this tutorial.

To get data from the `Member` model, we will have to import it in the `views.py` file, and extract data from it in the view:

`members/views.py`:

```jsx
from django.http import HttpResponse, HttpResponseRedirect from django.template import loader from .models import Member def testing(request): mymembers = Member.objects.all().values() template = loader.get_template('template.html') context = { 'mymembers': mymembers, } return HttpResponse(template.render(context, request))
```

Now we can use the data in the template:

`templates/template.html`:

```django
<ul> {% for x in mymembers %} <li>{{ x.firstname }}</li> {% endfor %} </ul>
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_variables4)

We use the Django template tag `{% for %}` to loop through the members.

You will learn more about [template tags](https://www.w3schools.com/django/django_template_tags.php) in the next chapter.

___

W3schools Pathfinder

Track your progress - it's free!

   [![Get Certified](https://www.w3schools.com/images/img_program_up_300.png)](https://campus.w3schools.com/collections/course-catalog/products/front-end-course)