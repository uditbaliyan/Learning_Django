___

## Add Records

The Members table created in the [previous chapter](https://www.w3schools.com/django/django_models.php) is empty.

We will use the Python interpreter (Python shell) to add some members to it.

To open a Python shell, type this command:

Now we are in the shell, the result should be something like this:

Python 3.9.2 (tags/v3.9.2:1a79785, Feb 19 2021, 13:44:55) \[MSC v.1928 64 bit (AMD64)\] on win32  
Type "help", "copyright", "credits" or "license" for more information.  
(InteractiveConsole)  
\>>>

At the bottom, after the three `>>>` write the following:

\>>> from members.models import Member

Hit \[enter\] and write this to look at the empty Member table:

This should give you an empty QuerySet object, like this:

A QuerySet is a collection of data from a database.

Read more about QuerySets in the [Django QuerySet](https://www.w3schools.com/django/django_queryset.php) chapter.

Add a record to the table, by executing these two lines:

\>>> member = Member(firstname='Emil', lastname='Refsnes')  
\>>> member.save()

Execute this command to see if the Member table got a member:

\>>> Member.objects.all().values()

Hopefully, the result will look like this:

<QuerySet \[{'id': 1, 'firstname': 'Emil', 'lastname': 'Refsnes'}\]>

___

## Add Multiple Records

You can add multiple records by making a list of `Member` objects, and execute `.save()` on each entry:

\>>> member1 = Member(firstname='Tobias', lastname='Refsnes')  
\>>> member2 = Member(firstname='Linus', lastname='Refsnes')  
\>>> member3 = Member(firstname='Lene', lastname='Refsnes')  
\>>> member4 = Member(firstname='Stale', lastname='Refsnes')  
\>>> member5 = Member(firstname='Jane', lastname='Doe')  
\>>> members\_list = \[member1, member2, member3, member4, member5\]  
\>>> for x in members\_list:  
\>>>   x.save()

Now there are 6 members in the Member table:

\>>> Member.objects.all().values()  
<QuerySet \[{'id': 1, 'firstname': 'Emil', 'lastname': 'Refsnes'},  
{'id': 2, 'firstname': 'Tobias', 'lastname': 'Refsnes'},  
{'id': 3, 'firstname': 'Linus', 'lastname': 'Refsnes'},  
{'id': 4, 'firstname': 'Lene', 'lastname': 'Refsnes'},  
{'id': 5, 'firstname': 'Stale', 'lastname': 'Refsnes'},  
{'id': 6, 'firstname': 'Jane', 'lastname': 'Doe'}\]>

___

