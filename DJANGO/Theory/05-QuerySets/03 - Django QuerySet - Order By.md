___

## Order By

To sort QuerySets, Django uses the `order_by()` method:

In SQL, the above statement would be written like this:

```sql
SELECT * FROM members ORDER BY firstname;
```

___

## Descending Order

By default, the result is sorted ascending (the lowest value first), to change the direction to descending (the highest value first), use the minus sign (NOT), `-` in front of the field name:

### Example

Order the result firstname descending:

```jsx
mydata = Member.objects.all().order_by('-firstname').values()
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_queryset_orderby2)

In SQL, the above statement would be written like this:

```sql
SELECT * FROM members ORDER BY firstname DESC;
```

___

## Multiple Order Bys

To order by more than one field, separate the fieldnames with a comma in the `order_by()` method:

### Example

Order the result first by lastname ascending, then descending on id:

```jsx
mydata = Member.objects.all().order_by('lastname', '-id').values()
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_queryset_orderby3)

In SQL, the above statement would be written like this:

```sql
SELECT * FROM members ORDER BY lastname ASC, id DESC;
```

___

W3schools Pathfinder

Track your progress - it's free!