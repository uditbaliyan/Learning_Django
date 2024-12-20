___

A Django model is a table in your database.

___

## Django Models

Up until now in this tutorial, output has been static data from Python or HTML templates.

Now we will see how Django allows us to work with data, without having to change or upload files in the prosess.

In Django, data is created in objects, called Models, and is actually tables in a database.

___

## Create Table (Model)

To create a model, navigate to the `models.py` file in the `/members/` folder.

Open it, and add a `Member` table by creating a `Member` `class`, and describe the table fields in it:

`my_tennis_club/members/models.py`:

```python
from django.db import models 
class Member(models.Model):
	firstname = models.CharField(max_length=255)
	lastname = models.CharField(max_length=255)
```

The first field, `firstname`, is a Text field, and will contain the first name of the members.

The second field, `lastname`, is also a Text field, with the member's last name.

Both `firstname` and `lastname` is set up to have a maximum of 255 characters.

## SQLite Database

When we created the Django project, we got an empty SQLite database.

It was created in the `my_tennis_club` root folder, and has the filename `db.sqlite3`.

By default, all Models created in the Django project will be created as tables in this database.

___

## Migrate

Now when we have described a Model in the `models.py` file, we must run a command to actually create the table in the database.

Navigate to the `/my_tennis_club/` folder and run this command:
```

py manage.py makemigrations members
```

Which will result in this output:

Migrations for 'members':  
  members\\migrations\\0001\_initial.py  
    - Create model Member

(myworld) C:\\Users\\_Your Name_\\myworld\\my\_tennis\_club>

Django creates a file describing the changes and stores the file in the `/migrations/` folder:

`my_tennis_club/members/migrations/0001_initial.py`:

```python
# Generated by Django 4.1.2 on 2022-10-27 11:14 
from django.db import migrations, models 
class Migration(migrations.Migration): 
initial = True dependencies = [ ] 
operations = [ migrations.CreateModel( name='Member', fields=[ ('id', models.BigAutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')), ('firstname', models.CharField(max_length=255)), ('lastname', models.CharField(max_length=255)), ], ), ]
```

Note that Django inserts an `id` field for your tables, which is an `auto increment number` (first record gets the value 1, the second record 2 etc.), this is the default behavior of Django, you can override it by describing your own `id` field.

The table is not created yet, you will have to run one more command, then Django will create and execute an SQL statement, based on the content of the new file in the `/migrations/` folder.


Now you have a `Member` table in you database!

___

## View SQL

As a side-note: you can view the SQL statement that were executed from the migration above. All you have to do is to run this command, with the migration number:
```

py manage.py sqlmigrate members 0001
```

Which will result in this output:

BEGIN;  
\--  
\-- Create model Member  
\--  
CREATE TABLE "members\_member" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "firstname" varchar(255) NOT NULL, "lastname" varchar(255) NOT NULL); COMMIT;

___
