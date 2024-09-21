___

## Comments

Comments allows you to have sections of code that should be ignored.

___

## Comment Description

You can add a message to your comment, to help you remember why you wrote the comment, or as message to other people reading the code.

### Example

Add a description to your comment:

```django
<h1>Welcome Everyone</h1> {% comment "this was the original welcome message" %} <h1>Welcome ladies and gentlemen</h1> {% endcomment %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_comment2)

___

## Smaller Comments

You can also use the `{# ... #}` tags when commenting out code, which can be easier for smaller comments:

### Example

Comment out the word Everyone:

```django
<h1>Welcome{# Everyone#}</h1>
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_comment3)

___

## Comment in Views

Views are written in Python, and Python comments are written with the `#` character:

### Example

Comment out a section in the view:

```jsx
from django.http import HttpResponse from django.template import loader def testing(request): template = loader.get_template('template.html') #context = { # 'var1': 'John', #} return HttpResponse(template.render())
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_comment4)

Read more about Python Comments in out [Python Comment Tutorial](https://www.w3schools.com/python/python_comments.asp).

___

W3schools Pathfinder

Track your progress - it's free!