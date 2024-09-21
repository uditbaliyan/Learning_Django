___

## Add Fields in the Model

To add a field to a table after it is created, open the `models.py` file, and make your changes:

`my_tennis_club/members/models.py`:

```jsx
from django.db import models class Member(models.Model): firstname = models.CharField(max_length=255) lastname = models.CharField(max_length=255) phone = models.IntegerField() joined_date = models.DateField()
```

As you can see, we want to add `phone` and `joined_date` to our Member Model.

This is a change in the Model's structure, and therefor we have to make a migration to tell Django that it has to update the database:

py manage.py makemigrations members

Which, in my case, will result in a prompt, because I try to add fields that are not allowed to be null, to a table that already contains records.

As you can see, Django asks if I want to provide the fields with a specific value, or if I want to stop the migration and fix it in the model:

py manage.py makemigrations members  
You are trying to add a non-nullable field 'joined\_date' to members without a default; we can't do that (the database needs something to populate existing rows).  
Please select a fix:  
 1) Provide a one-off default now (will be set on all existing rows with a null value for this column)  
 2) Quit, and let me add a default in models.py  
Select an option:

I will select option 2, and open the `models.py` file again and allow NULL values for the two new fields:

`my_tennis_club/members/models.py`:

```jsx
from django.db import models class Member(models.Model): firstname = models.CharField(max_length=255) lastname = models.CharField(max_length=255) phone = models.IntegerField(null=True) joined_date = models.DateField(null=True)
```

And make the migration once again:

py manage.py makemigrations members

Which will result in this:

Migrations for 'members':  
  members\\migrations\\0002\_member\_joined\_date\_member\_phone.py  
    - Add field joined\_date to member  
    - Add field phone to member

Run the migrate command:

Which will result in this output:

Operations to perform:  
  Apply all migrations: admin, auth, contenttypes, members, sessions  
Running migrations:  
  Applying members.0002\_member\_joined\_date\_member\_phone... OK

(myworld) C:\\Users\\_Your Name_\\myworld\\my\_tennis\_club>

___

## Insert Data

We can insert data to the two new fields with the same approach as we did in the [Update Data chapter](https://www.w3schools.com/django/django_update_data.php):

First we enter the Python Shell:

Now we are in the shell, the result should be something like this:

Python 3.9.2 (tags/v3.9.2:1a79785, Feb 19 2021, 13:44:55) \[MSC v.1928 64 bit (AMD64)\] on win32  
Type "help", "copyright", "credits" or "license" for more information.  
(InteractiveConsole)  
\>>>

At the bottom, after the three `>>>` write the following (and hit \[enter\] for each line):

\>>> from members.models import Member  
\>>> x = Member.objects.all()\[0\]  
\>>> x.phone = 5551234  
\>>> x.joined\_date = '2022-01-05'  
\>>> x.save()

This will insert a phone number and a date in the Member Model, at least for the first record, the four remaining records will for now be left empty. We will deal with them later in the tutorial.

Execute this command to see if the Member table got updated:

\>>> Member.objects.all().values()

The result should look like this:

<QuerySet \[  
{'id': 1, 'firstname': 'Emil', 'lastname': 'Refsnes', 'phone': 5551234, 'joined\_date': datetime.date(2022, 1, 5)},  
{'id': 2, 'firstname': 'Tobias', 'lastname': 'Refsnes', 'phone': None, 'joined\_date': None},  
{'id': 3, 'firstname': 'Linus', 'lastname': 'Refsnes', 'phone': None, 'joined\_date': None},  
{'id': 4, 'firstname': 'Lene', 'lastname': 'Refsnes', 'phone': None, 'joined\_date': None},  
{'id': 5, 'firstname': 'Stalikken', 'lastname': 'Refsnes', 'phone': None, 'joined\_date': None}\]>

___

W3schools Pathfinder

Track your progress - it's free!

   [![Get Certified](https://www.w3schools.com/images/img_certification_up_generic_django_300.png)](https://campus.w3schools.com/collections/certifications/products/django-certification-exam)