# An Introduction to Intermediate Python
*A compact introduction to some intermediate Python concepts.*

Python is one of the most popular programming languages in the world and is commonly learnt as a first programming language. As such, there are an abundance of courses, books and videos on learning basic Python. [This](https://howieko.com/post/python_mooc/) useful blog post by Howard Ko, which compares nine Python courses, can be used as a nice starting point.

Rather than simply being another guide on basic Python, this one aims to present some intermediate Python concepts in a compact way for someone who is already familiar with the basics of functional programming in Python.

Note that this guide is for Python 3, but can easily be translated into Python 2.

## Table of Contents

- [Code Standards](#code-standards)
  * [Indentation](#indentation)
  * [Comments](#comments)
    + [Inline Comments](#inline-comments)
    + [Block Comments](#block-comments)
  * [Docstrings](#docstrings)
    + [One-Line Docstrings](#one-line-docstrings)
    + [Multi-Line Docstrings](#multi-line-docstrings)
  * [Quotes](#quotes)
  * [Names](#names)
- [Quick Useful Python](#quick-useful-python)
  * [Handling Exceptions](#handling-exceptions)
  * [Aggregating Iterables](#aggregating-iterables)
  * [Using `in` With `print()`](#using-in-with-print)
  * [List Comprehension](#list-comprehension)
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
- [Object-Oriented Programming](#object-oriented-programming)
  * [Classes, Objects and Methods](#classes-objects-and-methods)
    + [Types](#types)
    + [Classes](#classes)
    + [Instantiation](#instantiation)
    + [Objects](#objects)
    + [Class Variables](#class-variables)
    + [Instance Variables](#instance-variables)
    + [Attributes](#attributes)
    + [Methods](#methods)
    + [Dunder Methods](#dunder-methods)
      - [Constructors](#constructors)
      - [String Representation](#string-representation)
    + [Using `self`](#using-self)
    + [(Almost) Everything is an Object](#almost-everything-is-an-object)
    + [Abstraction and Encapsulation](#abstraction-and-encapsulation)
  * [Inheritance and Polymorphism](#inheritance-and-polymorphism)
    + [Inheritance](#inheritance)
    + [Overriding](#overriding)
    + [The `super()` Function](#the-super-function)
    + [The `Exception` Class](#the-exception-class)
    + [Interfaces](#interfaces)
    + [Polymorphism](#polymorphism)
- [Decorators](#decorators)
  * [Functions Within Functions](#functions-within-functions)
  * [Decorating a Function](#decorating-a-function)
  * [Using Decorators](#using-decorators)
  * [Decorators with Parameters](#decorators-with-parameters)

## Code Standards

All written code should follow a style guide to ensure that standards are kept consistent across any codebase and make code easier to read. Badly written code is difficult to scale, optimise, and debug. Such is the importance of high code standards that this guide will discuss it as a separate section before any code is seen. Any new terminology or concepts mentioned in this section will be properly covered later in the guide.

We follow the standards in the [PEP 8 Style Guide](https://www.python.org/dev/peps/pep-0008/). In particular, this section will act as a reference for language-specific best practices for indentation, comments, quotes, and names, since these can vary across different programming languages.

### Indentation

The standard is to use four spaces for indented code.

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

Similar but different to comments, a *docstring* is a string that appears as the first statement in a module, function, class, or method definition, and is used to document what they do. Docstrings are usually used for modules, and all classes and functions exported by that module.

Docstrings should be wrapped with triple double quotes `""" """` and there should be a blank line after all docstrings that document a class. Best standards for docstrings can be read about in more detail [here](https://www.python.org/dev/peps/pep-0257/).

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

### Quotes

Whenever quotation marks are required in code, either consistently use double quotes `" "` or consistently use single quotes `' '` throughout the code. However, when a string contains double quotes or single quotes, then the choice of wrapping quotation marks should be such that the use of the escape character `\` is avoided.

Quotation marks for triple-quoted strings should always use double quotes.

### Names

Unfortunately there is no convention for general names. However, in this section we list the convention for common types of names. Best standards for names can be read about in more detail [here](https://www.python.org/dev/peps/pep-0008/#naming-conventions).

- Modules: Use short snake_case names.
- Packages: Use short lowercase names. Only use snake_case if necessary.
- Classes: Use PascalCase.
- Functions: Use snake_case.
- Variables: Use snake_case.
- Constants: Use uppercase. Any word separation should be done with an underscore `_`.

## Quick Useful Python

This section contains some quick useful pieces of Python which may not have been covered in a basic Python course.

### Handling Exceptions

It is generally better to handle exceptions by not letting them occur in the first place. However, this isn't always possible. As part of the debugging process, instead of letting the program crash, we can catch errors using a `try` and `except` block. Additionally, errors can be specified for the `except` block. Optionally, we can use an `else` block which executes if no errors were caught, and we can also use a `finally` block which executes regardless of whether any of the previous blocks were executed.

```Python
def division(x, y):
    return x/y

try:
    division(3, 0)
except ZeroDivisionError:
    print("You cannot divide by zero")
except:
    print("Something else went wrong")
else:
    print("Nothing went wrong")
finally:
    print("The try/except/else blocks have finished")
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

Similar to a dictionary, sets must also contain unique elements. We can use this to achieve the same aim of removing duplicates from a list without even needing to worry about immutability.

```Python
list(set(list_name))
```

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

In the following example the first function call returns `12`, the second function call returns `3`, and the third function call returns `128`:

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

The following example prints each word in uppercase:

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

## Object-Oriented Programming

Most initial users of Python create and implement their programs using functional factors, i.e. variables and functions are the central elements of the code. This is known as *functional programming* and uses the [*declarative programming model*](https://en.wikipedia.org/wiki/Declarative_programming). This section will be about another programming paradigm called *Object-Orient Programming (OOP)* which uses the [*imperative programming model*](https://en.wikipedia.org/wiki/Imperative_programming). In OOP the central elements are *objects* and methods.

There are four principles of OOP: abstraction, encapsulation, inheritance, and polymorphism. The first two are briefly discussed in [this section](#abstraction-and-encapsulation), and the final two are covered in more detail in [this section](#inheritance-and-polymorphism).

OOP can prove initially tricky to grasp, especially if only functional programming has been seen before. However, the main benefit of OOP is the structure that it offers, thereby allowing for programming projects that span multiple lines of code (and possibly collaborators) to be organised, understood, and developed in a more systematic way than would have been possible with only functional programming.

### Classes, Objects and Methods

We will now introduce several definitions and concepts which are core to OOP.

#### Types

Recall that Python has different data types such as `float`,` int`, `list` and `dict`, and that these are often stored in variables. The type of a Python variable can be checked using the `type()` function. A variable's type determines what we can do with it, and interactions with variables are defined at the type level. For example, we can't use the `.get()` method on an `int`, nor can we use `+` on two variables with the `dict` data type.

#### Classes

A *class* is a template for a data type, i.e. creating a class allows you to create your own data type, including the kind of information that it can hold and the possible interactions.

To define a class, use the `class` keyword.

```Python
class RandomClass:
    # The body of the class goes here.
```

#### Instantiation

For functions to be used, they must be called. Similarly, for classes to be used, they must be *instantiated*, i.e. we must create an *instance* of the class. This can be done as follows:

```Python
RandomClass()
```

Rather than simply instantiating a class, it is often more useful to store the instance in a variable for later access. Hence, the following is preferred:

```Python
random_instance = RandomClass()
```

#### Objects

An *object* is a collection of variables, and methods that can act on those variables. A class instance is an example of an object (we will soon define methods within classes). In particular, instantiation is the process of turning a class into an object.

When applied to an object, the `type()` function is essentially the converse of instantiation - it turns an object into a class. Consider the following example:

```Python
print(type(random_instance))  # Print: <class '__main__.RandomClass'>
```

Here `__main__` means the file that is currently being run, so the printout means that `random_instance` is an instance of the class `RandomClass`that was defined in the file that is currently being run.

#### Class Variables

A *class variable* is a variable that is the same for every instance of the class. This can be defined within the body of the class, and then accessed using the `object.class_variable` syntax. The following example demonstrates this:

```Python
class RaceCar:
    speed = "Very fast"

ferrari = RaceCar()
mercedes = RaceCar()

print(ferrari.speed)  # Print: Very fast
print(mercedes.speed)  # Print: Very fast
```

#### Instance Variables

An *instance variable* is a variable specific to the class instance which it is attached to. This is in contrast to a class variable. Accessing an instance variable is done by using the `object.instance_variable` syntax. The following example demonstrates this.

```Python
class MathsFormula:
    pass

formula1 = MathsFormula()
formula2 = MathsFormula()

formula1.length = "Quite long"
formula2.length = "Extremely short"

print(formula1.length)  # Print: Quite long
print(formula2.length)  # Print: Extremely short
```

#### Attributes

An *attribute* is an umbrella term for both class variables and instance variables. Notice that the syntax for accessing either a class or instance variable are essentially identical.

Attempting to access a non-existent attribute of an object will throw an `AttributeError`. To safely access attributes, we can use the `getattr()` function which allows us to pass an optional argument which specifies what to return if the attribute doesn't exist (instead of throwing an `AttributeError`).

```Python
getattr(some_instance, "random_attribute", 42)  # Default print: 42
```

If we just want to check if the attribute exists, then we can use the `hasattr()` function, which returns `True` if the attribute exists, and `False` otherwise.

```Python
hasattr(some_instance, "random_attribute")
```

The `dir()` function can be used to return a list of all of an object's attributes, including [dunder methods](#dunder-methods) (covered in a later section).

```Python
print(dir(object_name))  # Print a long list of all attributes
```

#### Methods

A *method* is a function defined as part of a class. The first parameter in a method signature will always refer to the object that is calling the method, and this is implicitly and automatically passed when the method is called. By convention, this parameter is named `self`.

Methods are defined similarly to functions, but must be indented as part of a class.

```Python
class RaceCar:
    def fuel(self):
        print("Not enough!")

mclaren = RaceCar()
mclaren.fuel()  # Print: Not enough!
```

If our class has a class variable, then we refer to it within the body of the class using the `self.class_variable` syntax.

```Python
class Circle:
    pi = 3.14

    def important_number(self):
        print("The important number is:", self.pi)

shape = Circle()
shape.important_number()  # Print: The important number is: 3.14
```

Similarly, if we wanted to call a method within the same class, then we would use the `self.method` syntax.

Notice that accessing an attribute and calling a method uses essentially the same syntax of `object.attribute_or_method`. This general syntax also covers the usage of `self` since it refers to an object.

Method signatures can accept more parameters than just `self`. The following example demonstrates this:

```Python
class Square:
    def area(self, length):
        return length**2

shape = Square()
print(shape.area(3))  # Print: 9
```

#### Dunder Methods

In addition to defining our own methods in classes, we can use Python's special methods which are wrapped in double-underscores `__`. These special methods are referred to as `magic methods` or `dunder methods` (an abbreviation from double-underscore method). Dunder methods can be used to enrich class behaviour and behave differently from regular methods.

In this section we will look at the `__init__` and `__repr__` dunder methods, but the full list of dunder methods can be found [here](https://docs.python.org/3/reference/datamodel.html#special-method-names).

##### Constructors

A *constructor* is a method which is called when a class is instantiated. In Python this usually refers to the `__init__` dunder method which initialises a class instance in a way that we define. In particular, the dunder method is called every time the class is instantiated. The following example demonstrates this:

```Python
class RaceCar:
    def __init__(self):
        print("vrooooom")

ferrari = RaceCar()  # Print: vrooooom
mercedes = RaceCar()  # Print: vrooooom
```

We may also pass arguments when a class is instantiated. These arguments will be passed to `__init__`. Modifying the above example:

```Python
class RaceCar:
    def __init__(self, car_name):
        print("vrooooom goes the", car_name)

ferrari = RaceCar("Ferrari")  # Print: vrooooom goes the Ferrari
mercedes = RaceCar("Mercedes")  # Print: vrooooom goes the Mercedes
```

##### String Representation

The `print()` function is extremely useful for debugging code, so classes should be created with this in mind. However, using `print()` on an object that has been created from a class instance returns the default string representation `<__main__.class_name object at memory_location>`, which isn't particularly useful for debugging.

To resolve this issue, we can use the `__repr__` dunder method which allows us to define the string representation. This dunder method can only have `self` as its parameter and must return a string. Modifying the previous example:

```Python
class RaceCar:
    def __init__(self, car_name):
        self.name = car_name  # Create an instance variable

    def __repr__(self):
        return "This car is a " + self.name

ferrari = RaceCar("Ferrari")
print(ferrari)  # Print: This car is a Ferrari
```

Our above usage of `self` within the `__init__` dunder method will be discussed in the next section.

#### Using `self`

We have already seen that we can create instance variables outside of the indented block of class code. It can sometimes be useful to create instance variables upon class instantiation by using the constructor. For example, if we can guarantee rigidity to the data that an object holds, such as a name or URL, then this may be desirable for convenience and code readability.

We have already seen an example of this in the previous section. Here we also present another example for the scenario where we create instance variables of some properties of some squares.

```Python
class Square:
    def __init__(self, length):
        self.length = length
        self.area = self.length**2
        self.perimeter = self.length*4

small_square = Square(2)
big_square = Square(10)

print(small_square.length)  # Print: 2
print(big_square.perimeter)  # Print: 40
print(small_square.area)  # Print: 4
```

Of course, we could have just created an area and perimeter method to produce the same result, but for some simple shape properties this is a more sensible and meaningful approach which reduces on code bloat.

#### (Almost) Everything is an Object

With the initial introduction to OOP out of the way, we can now go deeper with some of this programming paradigm's concepts. The interested reader is free to do their own research on the new terminology and concepts used in this section - some hyperlinks will be available to guide this.

So far we have seen the following definition:

<p align="center">
An <i>object</i> is a collection of variables, and methods that can act on those variables.
</p>

In fact, a more general statement is true - objects are Python's [abstraction](https://en.wikipedia.org/wiki/Abstraction_(computer_science)#Abstraction_in_object_oriented_programming) for data, and all data in a Python program are represented either by objects or by relations between objects (see the [documentation](https://docs.python.org/3/reference/datamodel.html)). In other words, objects allow users to interact with data and use it without needing to actually know about the the underlying mechanics of the data itself.

Furthermore, functions and methods are [first-class objects](https://en.wikipedia.org/wiki/First-class_citizen). In particular, methods are [function objects](https://docs.python.org/3/c-api/method.html#method-objects) (also called [*functors*](https://en.wikipedia.org/wiki/Function_object)).

We have also seen the following definition:

<p align="center">
A <i>class</i> is a template for a data type, i.e. creating a class allows you to create your own data type, including the kind of information that it can hold and the possible interactions.
</p>

Again, a more general statement is true - a class is a code template for creating objects (see the [documentation](https://docs.python.org/3/tutorial/classes.html)).

#### Abstraction and Encapsulation

It is impossible to talk about objects and classes without briefly talking about abstraction and encapsulation. We will discuss both of these OOP principles from the perspective of Python. However, the interested reader can use the hyperlinks for a more general read.

[*Abstraction*](https://en.wikipedia.org/wiki/Abstraction_(computer_science)) refers to hiding the real implementation and complexity of an object within a class or interface (covered [later](#interfaces)), while only showing the essential features of the object such that a user only needs to know how to use it. A real world example would be a car (the object) not requiring the driver (the user) to actually understand the underlying mechanics to operate it.

[*Encapsulation*](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)) refers to the bundling of objects and relations between them, often to protect the code from external access. Examples of this include classes and modules.

### Inheritance and Polymorphism

In this section we will cover the two remaining principles of OOP in detail. The [inheritance](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) and [polymorphism](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)) hyperlinks can be used to guide a more general read on these principles.

#### Inheritance

*Inheritance* is where a class acquires the properties of another class. The class which does the acquiring is called the *child class* or *subclass*, and the class being acquired from is called the *parent class* or *base class*. This is useful when we want to create a new class that will simply be a variant of an existing class.

In the following example, the `UnitCircle` class is the parent class, and the `LargeCircle` class is the child class which adds the `colour` class variable:

```Python
class UnitCircle:
    pi = 3.14
    radius = 1

    def __init__(self):
        self.area = self.pi*(self.radius**2)
        self.perimeter = 2*self.pi*self.radius

class GreenCircle(UnitCircle):
    colour = "Green"
```

Note that we may also add new methods in this way.

The `issubclass()` function can be used to check if one class is a subclass of another class. It returns `True` if the first argument is a subclass of the second argument, and `False` otherwise. The general syntax is as follows:

```Python
issubclass(ChildClass, ParentClass)
```

#### Overriding

As seen in the previous section, new class variables and methods can be added to a parent class to create a child class via inheritance. These can also be completely redefined for the child class by doing an *override*.

In the following simple example, the `DoubleUnitCube` class is the parent class, and the `DoubleUnitSquare` class is the child class with the `dimensions` class variable overridden, and the `ImportantCalculation` method also overridden:

```Python
class DoubleUnitCube:
    length = 2
    dimensions = 3

    def ImportantCalculation(self):
        volume = self.length**self.dimensions
        return volume

class DoubleUnitSquare(DoubleUnitCube):
    dimensions = 2

    def ImportantCalculation(self):
        area = self.length**self.dimensions
        return area

a_cube = DoubleUnitCube()
a_square = DoubleUnitSquare()

print(a_cube.ImportantCalculation())  # Print: 8
print(a_square.ImportantCalculation())  # Print: 4
```

#### The `super()` Function

If we just want to add extra logic to a pre-existing method, then we can use the `super()` function. This function calls a method from the parent class as a temporary object of the parent class. We call this temporary object a *proxy object*.

In the following example the `Car` class is the parent class with a constructor which is built upon in the `SuperCar` class - the `weight` and `maximum_speed` instance variables are still created, but in addition to a new `turbo_boost` instance variable:

```Python
class Car:
    def __init__(self, weight, maximum_speed):
        self.weight = weight
        self.maximum_speed = maximum_speed

class SuperCar(Car):
    def __init__(self, weight, maximum_speed, turbo_boost):
       super().__init__(weight, maximum_speed)  # Call method as normal
       self.turbo_boost = turbo_boost
```

#### The `Exception` Class

Python has a built-in class called [`Exception`](https://docs.python.org/3/library/exceptions.html#Exception). All user-defined exceptions should inherit from this class. All built-in, non-system-exiting exceptions also inherit from this class. (There is also another class called [`BaseException`](https://docs.python.org/3/library/exceptions.html#BaseException) which is the base class for all built-in exceptions, but user-defined classes should not inherit from this.)

The main benefit of allowing exceptions to inherit from one another is that we can choose to catch them at any level in our defined exception hierarchy. In the following example we create exceptions for starting a car:

```Python
class CarException(Exception):
    pass

class IgnitionException(CarException):
    pass

class SteeringException(CarException):
    pass

class GearboxException(CarException):
    pass
```

In the above example, if we wanted to catch an exception with a `try` and `except` block, instead of having to catch `CarException`, `IgnitionException` and `GearboxException`, we could just catch `CarException` instead depending on how granular we wish to be.

Using an exception hierarchy allows for greater control over the level of preciseness we wish to have. For the built-in exceptions, the hierarchy can be seen in the documentation [here](https://docs.python.org/3/library/exceptions.html#exception-hierarchy).

#### Interfaces

Sometimes it can be useful to have different classes with differently implemented methods to use the same method name. This is especially useful when we want an object, regardless of which class it is an instance of, to perform the same type of task.

In particular, classes are said to *implement the same interface* if they have the same method names and attributes. In Python, an *interface* refers to the names of the methods and the arguments that they take.

The following example demonstrates this:

```Python
class Dog:
    def print_animal(self):
        print("This is a dog")

class Husky(Dog):
    def print_animal(self):
        print("This is a Husky")

animal_A = Dog()
animal_B = Husky()

animal_A.print_animal()  # Print: This is a dog
animal_B.print_animal()  # Print: This is a Husky
```

For a more functional example, consider the following, where the `Chess` and `Checkers` classes implement the same interface, which we then use to do the same task of setting up a board game:

```Python
class Chess:
    def __init__(self):
        self.board = self.set_up_board()
        self.pieces = self.add_pieces()
        print("A game of chess is now ready to be played")

    def set_up_board(self):
        print("The chess board has been set up")

    def add_pieces(self):
        print("The chess pieces have been placed")

    def play(self):
        print("Now playing chess!")

class Checkers:
    def __init__(self):
        self.board = self.set_up_board()
        self.pieces = self.add_pieces()
        print("A game of checkers is now ready to be played")

    def set_up_board(self):
        print("The checkers board has been set up")

    def add_pieces(self):
        print("The checkers pieces have been placed")

    def play(self):
        print("Now checkers chess!")

def play_board_game(board_game):
    board_game.play()

chess_game = Chess()
checkers_game = Checkers()
another_chess_game = Chess()

for board_game in [chess_game, checkers_game, another_chess_game]:
    play_board_game(board_game)

# Print the following:
# The chess board has been set up
# The chess pieces have been placed
# A game of chess is now ready to be played
# The checkers board has been set up
# The checkers pieces have been placed
# A game of checkers is now ready to be played
# The chess board has been set up
# The chess pieces have been placed
# A game of chess is now ready to be played
# Now playing chess!
# Now checkers chess!
# Now playing chess!
```

#### Polymorphism

We've just seen that interfaces allow for flexibility in programming, but flexibility can also be introduced in other ways. For example, the `+` operator behaves differently depending on the data types that it is being used with, but does what we would intuitively expect it to do.

*Polymorphism* refers to the same syntax doing different actions depending on data type. This is a very general concept, but creating classes which implement the same interface is one way of introducing polymorphism into our code.

Another way to introduce polymorphism is to use dunder methods such as `__add__` to make our classes act like what we are already familiar with (recall the [dunder methods](#dunder-methods) section).

We will now look at an example which demonstrates the usefulness of dunder methods for adding intuition into code via polymorphism. Here we use the `__add__` dunder method to add together, using the `+` operator, two RGB colours (in the form of objects which are instances of the `Colour` class).

```Python
class Colour:
    def __init__(self, red, green, blue):
        self.red = red
        self.green = green
        self.blue = blue

    def __repr__(self):
        """Return the RGB colour code."""
        return  "RGB = ({red}, {green}, {blue})".format(red = self.red,
                                                        green = self.green,
                                                        blue = self.blue)

    def __add__(self, another_colour):
        """Allow for A + B to be used, instead of only A.__add__(B)."""
        red_value = min(self.red + another_colour.red, 255)
        green_value = min(self.green + another_colour.green, 255)
        blue_value = min(self.blue + another_colour.blue, 255)
        return Colour(red_value, green_value, blue_value)

red = Colour(255, 0, 0)
blue = Colour(0, 255, 0)
green = Colour(0, 0, 255)

magenta = red + blue
cyan = blue + green
yellow = red + green
white = red + green + blue

print(magenta)  # Print: RGB = (255, 255, 0)
print(cyan)  # Print: RGB = (0, 255, 255)
print(yellow)  # Print: RGB = (255, 0, 255)
print(white)  # Print: RGB = (255, 255, 255)
```

## Decorators

A *decorator* or *decorator function* is a special function which wraps existing functions to add extra functionality. These can be used in an extremely convenient way which make the reading and writing of our code easier.

In this section we start with some motivation before actually looking at decorators so that the benefit of using decorators is obvious.

### Functions Within Functions

Recall that functions are objects (see [this](#almost-everything-is-an-object) section), which means that it is possible to return functions from functions. For example, the following is perfectly valid:

```Python
def add_or_subtract_operation(operation):
    def add(x, y):
        return x + y
    def subtract(x, y):
        return x - y

    if operation == "+":
        return add
    elif operation == "-":
        return subtract
```

Note that in the above example, we return a **function** and not a **function call**.

### Decorating a Function

One way to decorate a function with additional functionality is to create a *wrapper function* which bundles the original function with additional functionality. In the following example, we create a decorator function `clean_decorator` which cleans an item:

```Python
def clean_decorator(item_function):
    def wrapper():
        print("A nice, clean and sparkly:")
        item_function()
    return wrapper

def print_ferrari():
    print("Ferrari")

def print_book():
    print("book")

decorated_ferrari_function = clean_decorator(print_ferrari)
decorated_book_function = clean_decorator(print_book)

decorated_ferrari_function()
# Print: A nice, clean and sparkly:
#        Ferrari

decorated_book_function()
# Print: A nice, clean and sparkly:
#        book
```

### Using Decorators

We can simplify the syntax in the previous section by using decorators. Instead of having to tediously create a function formed from calling the decorator function, and then calling that function, we can instead just use `@decorator_function` on the line before the function that we wish to decorate. This usage of decorators via the `@` symbol is an example of [*syntactic sugar*](https://en.wikipedia.org/wiki/Syntactic_sugar), i.e. syntax designed to make things easier to read or express.

Continuing from the previous example, our code can be simplified as follows:

```Python
def clean_decorator(item_function):
    def wrapper():
        print("A nice, clean and sparkly:")
        item_function()
    return wrapper

@clean_decorator
def print_ferrari():
    print("Ferrari")

@clean_decorator
def print_book():
    print("book")

print_ferrari()
print_book()
```

By abstracting away the underlying functions, it is now much clearer which functions we're actually interested in calling and decorating.

### Decorators with Parameters

So far we have been decorating functions defined without parameters. If we wish to have parameters in our function definitions, then we just need to ensure that these parameters are also accounted for in the wrapper function.

In the following example, we modify the previous example to have a `print_item()` function:

```Python
def clean_decorator(item_function):
    def wrapper(item_name):
        print("A nice, clean and sparkly:")
        item_function(item_name)
    return wrapper

@clean_decorator
def print_item(item_name):
    print(item_name)

print_item("table")
# Print: A nice, clean and sparkly:
#        table
```
