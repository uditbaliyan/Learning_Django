___

## Include

The `include` tag allows you to include a template inside the current template.

This is useful when you have a block of content that is the same for many pages.

### Example[Get your own Django Server](https://www.w3schools.com/django/django_server.php "W3Schools Spaces")

`templates/footer.html`:

```django
<p>You have reached the bottom of this page, thank you for your time.</p>
```

`templates/template.html`:

```django
<h1>Hello</h1> <p>This page contains a footer in a template.</p> {% include 'footer.html' %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_include)

___

## Variables in Include

You can send variables into the template by using the `with` keyword.

In the include file, you refer to the variables by using the `{{` _variablename_ `}}` syntax:

### Example

`templates/mymenu.html`:

```django
<div>HOME | {{ me }} | ABOUT | FORUM | {{ sponsor }}</div>
```

`templates/template.html`:

```django
<!DOCTYPE html> <html> <body> {% include "mymenu.html" with me="TOBIAS" sponsor="W3SCHOOLS" %} <h1>Welcome</h1> <p>This is my webpage</p> </body> </html>
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_include2)

___

W3schools Pathfinder

Track your progress - it's free!