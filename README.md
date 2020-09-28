# An Introduction to Intermediate Python
*A compact introduction to some intermediate Python concepts.*

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
- [Modules](#modules)
  * [Importing Particular Objects from a Module](#importing-particular-objects-from-a-module)
  * [Importing All Objects from a Module](#importing-all-objects-from-a-module)
- [Dictionary Methods](#dictionary-methods)
  * [Retrieval and Removal](#retrieval-and-removal)
  * [Dictionary View Objects](#dictionary-view-objects)
  * [A Neat Trick](#a-neat-trick)
- [Files](#files)
  * [Interactions](#interactions)
  * [Methods](#methods)
  * [CSV Files](#csv-files)
    + [Reading](#reading)
    + [Writing](#writing)
  * [JSON Files](#json-files)
    + [Reading](#reading-1)
    + [Writing](#writing-1)
- [Advanced Function Arguments](#advanced-function-arguments)
  * [Definitions](#definitions)
  * [Default Arguments](#default-arguments)
  * [Mutable Default Arguments](#mutable-default-arguments)
  * [Positional and Keyword Arguments](#positional-and-keyword-arguments)
  * [Unpacking Multiple Returns](#unpacking-multiple-returns)
  * [Positional and Keyword Argument Unpacking](#positional-and-keyword-argument-unpacking)
  * [Parameter and Argument Order](#parameter-and-argument-order)
  * [Passing Containers as Arguments](#passing-containers-as-arguments)
  
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

list_c = zip(list_a, list_b)
print(list_c)  # Print: [(1, "a"), (2, "b"), (3, "c")]
```

### Using `in` With `print()`

The `in` keyword can be used with the `print()` function to determine if a letter or substring exists in a string.

```Python
print("abc" in "abcdef")  # Print: True
print("abc" in "uvwxyz")  # Print: False
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

Inline comments should be used sparingly and not state the obvious. They should be separated by at least two spaces from the code and use commanding language rather than descriptive. For example, the following is preferred:

```Python
x = x + 1  # Compensate for border
```

As a comparison, the following should be avoided:

```Python
x = x + 1  # Compensates for border
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

One-line docstrings are for obvious cases. There should not be a blank line before or after the docstring, and it should be a phrase ending in a period which prescribes the function or method's effect as a command, not as a description. For example, the following is preferred:

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
    z -- the multiplier (default 4)
    """
    return x**y
```

## Modules

Modules allow for the usage of objects from outside of what's usually available. In fact, files are actually modules, so we can use the `import` keyword to access another file's contents within the same directory. Below we'll see various ways of using the `import` keyword.

### Importing Particular Objects from a Module

If we want to import and call a particular object from a module, then we can use the following syntax:

```Python
from module_name import object_name

object_name()
```

As seen [here](https://www.python.org/dev/peps/pep-0008/#imports), the stylistically correct way to import multiple objects from multiple modules is as follows (note the compression of objects onto one line and the separation of modules over multiple lines):

```Python
from module_name1 import object_name1, object_name2, object_name3
from module_name2 import object_nameA, object_nameB
```

We can also use the `as` keyword to give an imported object an alias. We can then call the object using its alias. In particular, using aliases can be useful when object names being imported conflict within our local namespace.

```Python
from module_name import object_name as alias_name

alias_name()
```

### Importing All Objects from a Module

Instead of importing objects one at a time from a module, we may also import them all at once. As we will see, this way of importing requires specifying the module (or its alias) every time we call any objects from it. This is useful if we want to call several different objects from the module and want clarity in the code on where these objects have originated from.

To import a module and call a particular object from that module, then we can use the following syntax:

```Python
import module_name

module_name.object_name()
```

Similar to the previous section, we can also use the `as` keyword to give the imported module an alias. We can then call a particular object from the module using the alias. Also similar to the previous section, using aliases can be useful when module names being imported conflict within our local namespace.

```Python
import module_name as alias_name

alias_name.object_name()
```

## Dictionary Methods

Recall that a dictionary is an unordered collection of data, stored as key-value pairs, and that keys must be an immutable data type, while values can be any data type.

### Retrieval and Removal

Recall also that accessing a value for a particular value can be done using the following syntax:

```Python
dictionary[key]
```

However, if the key does not exist then a `KeyError` will be thrown. To safely return values for keys, we can instead use the `get()` method. This will return `None` if the key does not exist, unless a second argument is specified.

```Python
dictionary.get(key)
```

The `list()` constructor returns a list of all keys in a dictionary.

```Python
list(dictionary)
```

The `pop()` method works like on a list - it removes a specified key (and hence its value), and returns the value corresponding to the removed key. If the key doesn't exist then a `KeyError` will be thrown, unless a second argument is specified (similar to the `get()` method).

```Python
dictionary.pop(key)
```

### Dictionary View Objects

Dictionary view objects can be iterated over and provide a window to look at the dictionary through. This is in contrast to `list()` which actually creates an object. The benefit is that only a small and fixed amount of memory and processing time is required, since a list does not need to be created.

The `keys()` method returns a dictionary view object of keys, with class `dict_keys`.

```Python
dictionary.keys()
```

The `values()` method returns a dictionary view object of values, with class `dict_values`.

```Python
dictionary.values()
```

The `items()` method returns a dictionary view object of tuples (key, value), with class `dict_items`.

```Python
dictionary.items()
```

Note that since dictionary view objects can be iterated over, the following equivalence holds:

```Python
list(dictionary.keys()) == list(dictionary)
```

### A Neat Trick

The `fromkeys()` method returns a dictionary with elements from the list as keys. Each key will have value `None`, unless a second argument is specified. The syntax is as follows:

```Python
dict.fromkeys(list_name)
```

This can be used to remove duplicates from a list.

```Python
list(dict.fromkeys(list_name))
```

Of course, the elements of the initial list must be immutable, but some further tricks can be used. For example, if an element of the list is a list, then we can convert it into a tuple, remove any duplicates, and then convert that element back into a list again.

## Files

Python is commonly used as a scripting language in industrial automation. In particular, it is common to want to automate interaction with different file types.

### Interactions

The `with` keyword creates a context manager, i.e. an indented block which can be used to work on an opened file, where leaving the indented block closes the file. This is often used in conjunction with the `open()` function to open a file. We can also include an optional second argument: `'r'` for read (the default), `'w'` for overwrite, `'a'` for append, and `'x'` for create.

```Python
with open('document.txt') as doc_name:
    doc_name.method()
```

### Methods

The `read()` method reads the file and returns its contents as a single string.

```Python
doc_name.read()
```

The `readlines()` method reads the file line by line and returns a list, where the elements are the lines.

```Python
doc_name.readlines()
```

The `readline()` method reads and returns one line of the file. Subsequent calls will read and return the next line. If there are no lines left, then the method will return an empty string.

```Python
doc_name.readline()
```

The `write()` method writes to the file.

```Python
doc_name.write()
```

### CSV Files

CSV (Comma-Separated Values) files are one of the most common file types in which data is stored. In a typical CSV file, the first line of data (i.e. the header) contains the labels of the data that's present in the rest of the file.

#### Reading

Consider a CSV file, named `people.csv`, which contains the following information:

```
id,name,age
1,Alice,20
2,Freddie,21
3,Bob,17
```

The `DictReader` class from the `csv` module can be used to convert each line into a dictionary. By default, the keys are the labels in the first line of the CSV file. It is also typical to pass the keyword argument `newline=''` to the `open()` function so that line breaks in data fields are interpreted correctly (see [here](https://docs.python.org/3/library/csv.html#id3) for further details).

```Python
import csv

with open('people.csv', newline='') as people_csv:
    people_reader = csv.DictReader(people_csv)
```

We can iterate over the `people_reader` reader object and print the results to better visualise the dictionaries. The stored dictionaries are sometimes referred to as *rows*.

```Python
{"id": "1", "name": "Alice", "age": "20"}
{"id": "2", "name": "Freddie", "age": "21"}
{"id": "3", "name": "Bob", "age": "17"}
```

Note that CSV files can use delimiters other than a comma, despite the name. This can be specified using the `delimiter` keyword argument.

```Python
csv.DictReader(another_csv, delimiter=';')
```

#### Writing

Consider a list of dictionaries, named `big_list`, which is defined as follows:

```Python
big_list = [{"id": "1", "name": "Alice", "age": "20"},
{"id": "2", "name": "Freddie", "age": "21"},
{"id": "3", "name": "Bob", "age": "17"}]
```

The `DictWriter` class from the `csv` module can be used to write to a (new) CSV file. We can specify the fields by passing the keyword argument `fieldnames=fields`, where `fields` should contain the keys from our list of dictionaries. This needs to be followed by using the `writeheader()` method on the writer object to pass the fields to the first row (i.e. creating the header), and then the `writerow()` method to write the rest of the information to the CSV file.

```Python
import csv

with open('output.csv', 'w') as output_csv:
    fields = ["id", "name", "age"]
    output_writer = csv.DictWriter(output_csv, fieldnames=fields)
    output_writer.writeheader()
    
    for item in big_list:
        output_writer.writerow(item)
```

### JSON Files

JSON (JavaScript Object Notation) files are another common file type in which data is stored. Since the format of a JSON file is similar to a CSV file, the handling of one is also similar.

#### Reading

Consider a JSON file, named `purchase_14781239.json`, which contains the following information:

```
{
    'user': 'ellen_greg',
    'action': 'purchase',
    'item_id': '14781239',
}
```
The `load()` method from the `json` module can be used to convert the JSON file into a dictionary.

```Python
import json

with open('purchase_14781239.json') as purchase_json
    purchase_data = json.load(purchase_json)
```

#### Writing

Consider a dictionary, named `turn_to_json`, which is defined as follows:

```Python
turn_to_json = {"user": "ellen_greg",
"action": "purchase",
"item_id": "14781239"}
```

The `dump()` method from the `json` module can be used to write to a (new) JSON file. The method takes two arguments: first the data object, and then the file object to write to.

```Python
import json

with open('output.json', 'w') as json_file:
    json.dump(turn_to_json, json_file)
```

## Advanced Function Arguments

It's impossible to use Python without arguments so it's safe to say that every Python user knows how to use them. However, it is possible to use Python without knowing about some of the finer details which are offered by Python's expressive function syntax. In fact, earlier in this guide there was some use of default arguments [here](#multi-line-docstrings) and keyword arguments [here](#csv-files).

### Definitions

Although some terms such as "argument" and "parameter" are used interchangeably in regular conversation, it helps to be precise with them for this section to make the most sense.

- A *function definition* begins with def and contains the entire following indented block.
- A *function call* is the place a function is invoked, with parentheses, after its definition.
- A *function signature* consists of the information between the initial parentheses in a function definition.
- A *parameter* is a variable in the function definition.
- An *argument* is the value being passed into a function call.

### Default Arguments

If two parameters are defined in a function definition, then when the function is called we must pass exactly two arguments. These are called *required parameters* or *positional parameters*.

By contrast, a *default argument* is an argument which may optionally be passed when a function is called, and defaults to a defined value otherwise. Note that any default values for parameters must be listed *after* any required parameters in a function signature. Sometimes these parameters are called *keyword parameters*.

Default arguments can be allowed by making their corresponding parameters have a default value. In the following example the first function call returns `4374` and the second function call returns `3`:

```Python
def example_function(x, y = 7, z = 2):
    return (x**y)*z

example_function(3)
example_function(1, 5, 3)
```

### Mutable Default Arguments

Unless there is a good reason to, **do not use mutable default arguments**. The following example demonstrates why:

```Python
def list_add(num, lst = []):
    lst.append(num)
    return lst

print(list_add(3))  # Print: [3]
print(list_add(4))  # Print: [3, 4], not [4]
print(list_add(5))  # Print: [3, 4, 5], not [5]
```

For a discussion on why this happens, see [here](https://stackoverflow.com/questions/1132941/least-astonishment-and-the-mutable-default-argument). To avoid this, simply use immutable default arguments. If we need to use an empty version of a data type, then we can use `None` as a sentinel.

The following example is the correct way to do the previous example:

```Python
def list_add(num, lst = None):
    if lst is None:
        lst = []
    lst.append(num)
    return lst
```

### Positional and Keyword Arguments

Typically when a function is called, we must pass arguments in the order in which the parameters are listed in the function signature. These passed arguments are called *positional arguments*.

If we want to pass arguments in any order, then we need to explicitly pass the name of parameters as arguments (along with their values). These explicitly named arguments are called *keyword arguments*.

Similar to function signatures, passing arguments in function calls must be done with keyword arguments *after* any positional arguments.

In the following example the first function call returns `12`,  the second function call returns `3`, and the third function call returns `128`:

```Python
def example_function(x, y = 7, z = 2):
    return (x**y)*z

example_function(3, z = 4, y = 1)
example_function(x = 3)
example_function(y = 3, x = 4, z = 2)
```

### Unpacking Multiple Returns

Functions can be made to return multiple pieces of data by separating them with a comma in the `return` statement. These are then stored in a tuple which can be indexed into. Alternatively, we can *unpack* the function return into separate variables, separated with a comma, in a single line.

The following example demonstrates this:

```Python
def example_function(x, y):
    sum_nums = x + y
    mult_nums = x*y
    return sum_nums, mult_nums

print(example_function(2, 5))  # Print: (7, 10)

sum_variable, mult_variable = example_function(2, 5)  # Unpack
print(sum_variable)  # Print: 7
print(mult_variable)  # Print: 10
```

### Positional and Keyword Argument Unpacking

If we want to allow for an indefinite number of arguments to be passed at function call, then we can use *argument unpacking*. For positional arguments this is called *positional argument unpacking*. Similarly, for keyword arguments this is called *keyword argument unpacking*.

To use positional argument unpacking, we use a parameter, typically `args` (by standard practice), suffixed by `*` in our function signature. Passed positional arguments will be packed into a tuple and stored in this parameter, which we can then interact with in the function definition. In this case, we call `*args` an *unpacked positional parameter*.

The following example prints each word in upper case:

```Python
def exclamation(*args):
    for argument in args:  # Unpack
        print(argument.upper())

exclamation("hello", "world", "goodbye", "boredom")
```

Similarly, to use keyword argument unpacking, we use a parameter, typically `kwargs`, suffixed by `**` in our function signature. Passed keyword arguments will be packed into a dictionary and stored in this parameter, which we can then interact with in the function definition (see the [Dictionary Methods section](#dictionary-methods)). In this case, we call `**kwargs` an *unpacked keyword parameter*.

The following example prints the value of a particular keyword argument:

```Python
def bills(**kwargs):
    print(kwargs.get("owed"))

bills(name = "Alice", city = "London", owed = 900)  # Print: 900
```

### Parameter and Argument Order

We can use a mix of all of the previously mentioned types of parameters, but this must be done in a particular order in the function signature:
- All non-unpacked positional parameters.
- An unpacked positional parameter.
- All non-unpacked keyword parameters.
- An unpacked keyword parameter.

Of course, any arguments passed into the function call must also follow this order.

### Passing Containers as Arguments

Recall that Python's container datatypes are: dictionary, list, set, and tuple.

Even if a function doesn't accept containers, we can pass them into the function call by deconstructing them in the call.

For functions which accept positional arguments, we can pass lists, sets, or tuples, by suffixing the container with `*` in the function call. The following example demonstrates this:

```Python
def addition(x, y, z):
    return x + y + z

print(addition(*[4, 9, 1]))  # Print: 14
```

For functions which accept keyword arguments, we can pass dictionaries by suffixing the container with `**` in the function call. The following example demonstrates this:

```Python
def powerful_addition(x = 7, y = 2, z = 5):
    return (x**y) + z

print(powerful_addition(**{"x": 3, "y": 5, "z": 9}))  # Print: 252
```
