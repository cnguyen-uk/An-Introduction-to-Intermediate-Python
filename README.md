# An Introduction to Intermediate Python
*A compact introduction to some intermediate Python concepts*

Python is one of the most popular programming languages in the world and is commonly learnt as a first programming language. As such, there are an abundance of courses, books and videos on learning basic Python. [This](https://howieko.com/post/python_mooc/) useful blog post by Howard Ko, which compares nine Python courses, can be used as a nice starting point.

Rather than simply being another guide on basic Python, this one aims to present some intermediate Python concepts in a compact way for someone who is already familiar with the basics of functional programming in Python.

Note that this guide is for Python 3, but can easily be translated into Python 2.

## Table of Contents

- [Quick Useful Python](#quick-useful-python)
  * [Handling Exceptions](#handling-exceptions)
  * [Aggregating Iterables](#aggregating-iterables)
  * [Using `in` With `print()`](#using-in-with-print)
  * [List Comprehension](#list-comprehension)

## Quick Useful Python

This section contains some quick useful pieces of Python which may not have been covered in a basic Python course.

### Handling Exceptions

It is generally better to handle exceptions but not letting them occur in the first place. However, this isn't always possible. As part of the debugging process, instead of letting the program crash, we can catch errors using a `try` and `except` block. Additionally, errors can be specified for the `except` block. We can also use a `finally` block to execute code regardless of whether the `try` block raises an error.

```Python
def division(x, y):
	return x/y

try:
	division(3, 0)
except ZeroDivisionError:
	print("You cannot divide by zero")
except:
	print("Something else went wrong")
finally:
	print("The try/except block has finished")
```

### Aggregating Iterables

The `zip()` function can be used to aggregate iterables together. The length of the returned iterable is determined by the iterable with the shortest length.

```Python
list_a = [1, 2, 3, 4]
list_b = ["a", "b", "c"]

# This 
list_c = zip(list_a, list_b)  # Prints: [(1, "a"), (2, "b"), (3, "c")]
```

### Using `in` With `print()`

The `in` keyword can be used with the `print()` function to determine if a letter or substring exists in a string.

```Python
print("abc" in "abcdef")  # Prints: True
print("abc" in "uvwxyz")  # Prints: False
```

### List Comprehension

List comprehension allows for the creation of lists in a concise way. The basic syntax is as follows::

```Python
[expression for item in list if optional_conditional]
```

Expressions can be anything, and we can have as many `for` or `if` statements as we like, including zero.

Set and dictionary comprehension works in the same way.
