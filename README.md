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
  * [Comments](#comments)
    + [Inline Comments](#inline-comments)
    + [Block Comments](#block-comments)
  * [Docstrings](#docstrings)
    + [One-Line Docstrings](#one-line-docstrings)
    + [Multi-Line Docstrings](#multi-line-docstrings)

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

### Comments

Every Python course will cover how to comment, but not every course will discuss good standards for commenting. Good standards are important for consistency and accessibility for whoever is reading the code. Best standards for comments can be read about in more detail [here](https://www.python.org/dev/peps/pep-0008/#comments).

#### Inline Comments

Inline comments should be used sparingly and not state the obvious. They should be separated by at least two spaces from the code and use descriptive language rather than commanding. For example, the following is preferred:

```Python
x = x + 1  # Compensate for border
```

As a comparison, the following should be avoided:

```Python
x = x + 1 # Compensates for border
```

#### Block Comments

Block comments should be written in complete sentences, be indented with the code which it is commenting, and come *before* the code which it is commenting. Placing the comment after is merciless on a confused reader. Paragraphs are separated by a single line containing a single `#`, and multi-sentence comments should have two spaces after a sentence-ending period (except after the final sentence).

```Python
# This function triples a number.  It does not check for valid input.
#
# It's quite a nice function.
def triple(x):
	return 3*x
```

### Docstrings

Similar but different to comments, a docstring is a string that appears as the first statement in a module, function, class, or method definition, and is used to document what they do. Docstrings are usually used for modules, and all classes and functions exported by that module.

Triple double quotes should be used around docstrings and there should be a blank line after all docstrings that document a class. Best standards for docstrings can be read about in more detail [here](https://www.python.org/dev/peps/pep-0257/).

#### One-Line Docstrings

One-line docstrings are for obvious cases. They should be a phrase ending in a period and it should prescribs the function or method's effect as a command, not as a description. For example, the following is preferred:

```Python
def triple(x)
	"""Return the triple of a number."""
	return 3*x
```

As a comparison, the following should be avoided:

```Python
def triple(x)
	"""Returns the triple of a number."""
	return 3*x
```

#### Multi-Line Docstrings

Multi-line docstrings begin with a summary line, on the same line as the starting triple quotes, followed by a space, a more elaborate description, and then the ending triple quotes on a line by themselves. For example:

```Python
def power(x, y=2, z=4)
	"""Raise x to the power of y, then multiply by 4.
	
	Arguments:
	x -- the base number
	y -- the exponent (default 2)
	z -- the multiplier (defult 4)
	"""

	return x**y
```
