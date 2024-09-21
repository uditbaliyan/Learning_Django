___

## If Statement

An `if` statement evaluates a variable and executes a block of code if the value is true.

___

## Elif

The `elif` keyword says "if the previous conditions were not true, then try this condition".

### Example

```django
{% if greeting == 1 %} <h1>Hello</h1> {% elif greeting == 2 %} <h1>Welcome</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_elif)

___

## Else

The `else` keyword catches anything which isn't caught by the preceding conditions.

### Example

```django
{% if greeting == 1 %} <h1>Hello</h1> {% elif greeting == 2 %} <h1>Welcome</h1> {% else %} <h1>Goodbye</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_else)

___

## Operators

The above examples uses the `==` operator, which is used to check if a variable is equal to a value, but there are many other operators you can use, or you can even drop the operator if you just want to check if a variable is not empty:

### Example

```django
{% if greeting %} <h1>Hello</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator)

___

## \==

Is equal to.

### Example

```django
{% if greeting == 2 %} <h1>Hello</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_equal)

___

## !=

Is not equal to.

### Example

```django
{% if greeting != 1 %} <h1>Hello</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_notequal)

___

### <

Is less than.

### Example

```django
{% if greeting < 3 %} <h1>Hello</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_lessthan)

___

## <=

Is less than, or equal to.

### Example

```django
{% if greeting <= 3 %} <h1>Hello</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_lessthan_eq)

___

## \>

Is greater than.

### Example

```django
{% if greeting > 1 %} <h1>Hello</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_gt)

___

## \>=

Is greater than, or equal to.

### Example

```django
{% if greeting >= 1 %} <h1>Hello</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_gt_eq)

___

## and

To check if more than one condition is true.

### Example

```django
{% if greeting == 1 and day == "Friday" %} <h1>Hello Weekend!</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_and)

___

## or

To check if one of the conditions is true.

### Example

```django
{% if greeting == 1 or greeting == 5 %} <h1>Hello</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_or)

___

## and/or

Combine `and` and `or`.

### Example

```django
{% if greeting == 1 and day == "Friday" or greeting == 5 %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_andor)

Parentheses are not allowed in `if` statements in Django, so when you combine `and` and `or` operators, it is important to know that parentheses are added for `and` but not for `or`.

Meaning that the above example is read by the interpreter like this:

```django
{% if (greeting == 1 and day == "Friday") or greeting == 5 %}
```

___

## in

To check if a certain item is present in an object.

### Example

```django
{% if 'Banana' in fruits %} <h1>Hello</h1> {% else %} <h1>Goodbye</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_in)

___

## not in

To check if a certain item is not present in an object.

### Example

```django
{% if 'Banana' not in fruits %} <h1>Hello</h1> {% else %} <h1>Goodbye</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_notin)

___

## is

Check if two objects are the same.

This operator is different from the `==` operator, because the `==` operator checks the values of two objects, but the `is` operator checks the identity of two objects.

In the view we have two objects, `x` and `y`, with the same values:

### Example

`views.py`:

```jsx
from django.http import HttpResponse from django.template import loader def testing(request): template = loader.get_template('template.html') context = { 'x': ['Apple', 'Banana', 'Cherry'], 'y': ['Apple', 'Banana', 'Cherry'], } return HttpResponse(template.render(context, request))
```

The two objects have the same value, but is it the same object?

### Example

```django
{% if x is y %} <h1>YES</h1> {% else %} <h1>NO</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_is1)

Let us try the same example with the `==` operator instead:

### Example

```django
{% if x == y %} <h1>YES</h1> {% else %} <h1>NO</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_is2)

How can two objects be the same? Well, if you have two objects that points to the same object, then the `is` operator evaluates to true:

We will demonstrate this by using the `{% with %}` tag, which allows us to create variables in the template:

### Example

```django
{% with var1=x var2=x %} {% if var1 is var2 %} <h1>YES</h1> {% else %} <h1>NO</h1> {% endif %} {% endwith %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_is3)

___

## is not

To check if two objects are not the same.

### Example

```django
{% if x is not y %} <h1>YES</h1> {% else %} <h1>NO</h1> {% endif %}
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_templates_operator_isnot)

___

W3schools Pathfinder

Track your progress - it's free!

   [![Get Certified](https://www.w3schools.com/images/img_fullaccess_up_sep1_green_300.png)](https://campus.w3schools.com/products/w3schools-full-access-course)