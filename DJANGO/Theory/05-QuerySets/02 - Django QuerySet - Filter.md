___

## QuerySet Filter

The `filter()` method is used to filter your search, and allows you to return only the rows that matches the search term.

As we learned in the previous chapter, we can filter on field names like this:

In SQL, the above statement would be written like this:

```sql
SELECT * FROM members WHERE firstname = 'Emil';
```

___

## AND

The `filter()` method takes the arguments as \*\*kwargs (keyword arguments), so you can filter on more than one field by separating them by a comma.

### Example

Return records where lastname is "Refsnes" and id is 2:

```jsx
mydata = Member.objects.filter(lastname='Refsnes', id=2).values()
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_queryset_filter)

In SQL, the above statement would be written like this:

```sql
SELECT * FROM members WHERE lastname = 'Refsnes' AND id = 2;
```

___

## OR

To return records where firstname is Emil or firstname is Tobias (meaning: returning records that matches either query, not necessarily both) is not as easy as the AND example above.

We can use multiple `filter()` methods, separated by a pipe `|` character. The results will merge into one model.

### Example

Return records where firstname is either "Emil" or Tobias":

```jsx
mydata = Member.objects.filter(firstname='Emil').values() | Member.objects.filter(firstname='Tobias').values()
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_queryset_filter_or)

Another common method is to import and use Q expressions:

### Example

Return records where firstname is either "Emil" or Tobias":

```jsx
from django.http import HttpResponse from django.template import loader from .models import Member from django.db.models import Q def testing(request): mydata = Member.objects.filter(Q(firstname='Emil') | Q(firstname='Tobias')).values() template = loader.get_template('template.html') context = { 'mymembers': mydata, } return HttpResponse(template.render(context, request))
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_queryset_filter_q)

In SQL, the above statement would be written like this:

```sql
SELECT * FROM members WHERE firstname = 'Emil' OR firstname = 'Tobias';
```

___

## Field Lookups

Django has its own way of specifying SQL statements and WHERE clauses.

To make specific where clauses in Django, use "Field lookups".

Field lookups are keywords that represents specific SQL keywords.

### Example:

Use the `__startswith` keyword:

```jsx
.filter(firstname__startswith='L');
```

Is the same as the SQL statement:

```sql
WHERE firstname LIKE 'L%'
```

The above statement will return records where firstname starts with 'L'.

## Field Lookups Syntax

All Field lookup keywords must be specified with the fieldname, followed by two(!) underscore characters, and the keyword.

In our `Member` model, the statement would be written like this:

### Example

Return the records where `firstname` starts with the letter 'L':

```jsx
mydata = Member.objects.filter(firstname__startswith='L').values()
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_queryset_filter_startswith)

## Field Lookups Reference

A list of all field look up keywords:

| Keyword | Description |
| --- | --- |
| [contains](https://www.w3schools.com/django/ref_lookups_contains.php) | Contains the phrase |
| [icontains](https://www.w3schools.com/django/ref_lookups_icontains.php) | Same as contains, but case-insensitive |
| date | Matches a date |
| day | Matches a date (day of month, 1-31) (for dates) |
| [endswith](https://www.w3schools.com/django/ref_lookups_endswith.php) | Ends with |
| [iendswith](https://www.w3schools.com/django/ref_lookups_iendswith.php) | Same as endswidth, but case-insensitive |
| [exact](https://www.w3schools.com/django/ref_lookups_exact.php) | An exact match |
| [iexact](https://www.w3schools.com/django/ref_lookups_iexact.php) | Same as exact, but case-insensitive |
| [in](https://www.w3schools.com/django/ref_lookups_in.php) | Matches one of the values |
| isnull | Matches NULL values |
| [gt](https://www.w3schools.com/django/ref_lookups_gt.php) | Greater than |
| [gte](https://www.w3schools.com/django/ref_lookups_gte.php) | Greater than, or equal to |
| hour | Matches an hour (for datetimes) |
| [lt](https://www.w3schools.com/django/ref_lookups_lt.php) | Less than |
| [lte](https://www.w3schools.com/django/ref_lookups_lte.php) | Less than, or equal to |
| minute | Matches a minute (for datetimes) |
| month | Matches a month (for dates) |
| quarter | Matches a quarter of the year (1-4) (for dates) |
| [range](https://www.w3schools.com/django/ref_lookups_range.php) | Match between |
| regex | Matches a regular expression |
| iregex | Same as regex, but case-insensitive |
| second | Matches a second (for datetimes) |
| [startswith](https://www.w3schools.com/django/ref_lookups_startswith.php) | Starts with |
| [istartswith](https://www.w3schools.com/django/ref_lookups_istartswith.php) | Same as startswith, but case-insensitive |
| time | Matches a time (for datetimes) |
| week | Matches a week number (1-53) (for dates) |
| week\_day | Matches a day of week (1-7) 1 is sunday |
| iso\_week\_day | Matches a ISO 8601 day of week (1-7) 1 is monday |
| year | Matches a year (for dates) |
| iso\_year | Matches an ISO 8601 year (for dates) |

___

W3schools Pathfinder

Track your progress - it's free!

   [![Get Certified](https://www.w3schools.com/images/img_certification_up_generic_django_300.png)](https://campus.w3schools.com/collections/certifications/products/django-certification-exam)