___

## The extends Tag

In the previous pages we created two templates, one for listing all members, and one for details about a member.

The templates have a set of HTML code that are the same for both templates.

Django provides a way of making a "parent template" that you can include in all pages to do the stuff that is the same in all pages.

Start by creating a template called `master.html`, with all the necessary HTML elements:

### Master[Get your own Django Server](https://www.w3schools.com/django/django_server.php "W3Schools Spaces")

`my_tennis_club/members/templates/master.html`:

```django
<!DOCTYPE html> 
<html> 
	<head> 
		<title>
		{% block title %}
		{% endblock %}
		</title> 
	</head> 
		<body> 
		{% block content %} {% endblock %} 
		</body> 
</html>
```

Do you see Django block Tag inside the `<title>` element, and the `<body>` element?

They are placeholders, telling Django to replace this block with content from other sources.

___

## Modify Templates

Now the two templates (`all_members.html` and `details.html`) can use this `master.html` template.

This is done by including the master template with the `{% extends %}` tag, and inserting a `title` block and a `content` block:

### Members

`my_tennis_club/members/templates/all_members.html`:

```django
{% extends "master.html" %} {% block title %}
My Tennis Club - List of all members
{% endblock %} {% block content %}
<h1>Members</h1> 
<ul> {% for x in mymembers %} 
<li><a href="details/{{ x.id }}">{{ x.firstname }} {{ x.lastname }}</a></li>
{% endfor %} 
</ul> 
{% endblock %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_master_index)

### Details

`my_tennis_club/members/templates/details.html`:

```django
{% extends "master.html" %} {% block title %} 
Details about {{ mymember.firstname }} {{ mymember.lastname }} 
{% endblock %} {% block content %} 
<h1>{{ mymember.firstname }} {{ mymember.lastname }}</h1>
<p>Phone {{ mymember.phone }}</p>
<p>Member since: {{ mymember.joined_date }}</p>
<p>Back to <a href="/members">Members</a></p>
{% endblock %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_master_details1)

If you have followed all the steps on your own computer, you can see the result in your own browser: `[127.0.0.1:8000/members/](http://127.0.0.1:8000/members/)`.

If the server is down, you have to start it again with the `runserver` command:

___

