___

## Template Tags

In Django templates, you can perform programming logic like executing `if` statements and `for` loops.

These keywords, `if` and `for`, are called "template tags" in Django.

To execute template tags, we surround them in `{% %}` brackets.

___

## Django Code

The template tags are a way of telling Django that here comes something else than plain HTML.

The template tags allows us to to do some programming on the server before sending HTML to the client.

`templates/template.html`:

```django
<ul> {% for x in mymembers %} <li>{{ x.firstname }}</li> {% endfor %} </ul>
```

[Run Example »](https://www.w3schools.com/django/showdjango.php?filename=demo_variables4)

In the next chapters you will learn about the most common template tags.

___

## Tag Reference

A list of all template tags:

| Tag | Description |
| --- | --- |
| [autoescape](https://www.w3schools.com/django/ref_tags_autoescape.php) | Specifies if autoescape mode is on or off |
| [block](https://www.w3schools.com/django/ref_tags_block.php) | Specifies a block section |
| [comment](https://www.w3schools.com/django/ref_tags_comment.php) | Specifies a comment section |
| csrf\_token | Protects forms from Cross Site Request Forgeries |
| [cycle](https://www.w3schools.com/django/ref_tags_cycle.php) | Specifies content to use in each cycle of a loop |
| debug | Specifies debugging information |
| [extends](https://www.w3schools.com/django/ref_tags_extends.php) | Specifies a parent template |
| [filter](https://www.w3schools.com/django/ref_tags_filter.php) | Filters content before returning it |
| [firstof](https://www.w3schools.com/django/ref_tags_firstof.php) | Returns the first not empty variable |
| [for](https://www.w3schools.com/django/ref_tags_for.php) | Specifies a for loop |
| [if](https://www.w3schools.com/django/ref_tags_if.php) | Specifies a if statement |
| [ifchanged](https://www.w3schools.com/django/ref_tags_ifchanged.php) | Used in for loops. Outputs a block only if a value has changed since the last iteration |
| [include](https://www.w3schools.com/django/ref_tags_include.php) | Specifies included content/template |
| load | Loads template tags from another library |
| [lorem](https://www.w3schools.com/django/ref_tags_lorem.php) | Outputs random text |
| [now](https://www.w3schools.com/django/ref_tags_now.php) | Outputs the current date/time |
| [regroup](https://www.w3schools.com/django/ref_tags_regroup.php) | Sorts an object by a group |
| [resetcycle](https://www.w3schools.com/django/ref_tags_resetcycle.php) | Used in cycles. Resets the cycle |
| [spaceless](https://www.w3schools.com/django/ref_tags_spaceless.php) | Removes whitespace between HTML tags |
| [templatetag](https://www.w3schools.com/django/ref_tags_templatetag.php) | Outputs a specified template tag |
| url | Returns the absolute URL part of a URL |
| [verbatim](https://www.w3schools.com/django/ref_tags_verbatim.php) | Specifies contents that should not be rendered by the template engine |
| widthratio | Calculates a width value based on the ratio between a given value and a max value |
| [with](https://www.w3schools.com/django/ref_tags_with.php) | Specifies a variable to use in the block |

___

W3schools Pathfinder

Track your progress - it's free!

   [![Get Certified](https://www.w3schools.com/images/img_package_up_300.png)](https://campus.w3schools.com/collections/package-deals)