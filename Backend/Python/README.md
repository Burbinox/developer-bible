# Python
- [.lock file](#lock_file)
- [Abstraction in Python](#abstraction_in_python)
- [Asterisk in function definition ](#asterisk_in_function_definition)
- [@classmethod and @staticmethod](#classmethod_and_staticmethod)
- [Code quality](#code_quality)
- [Composition vs Inheritance](#composition_vs_inheritance)
- [Context Managers](#context_managers)
- [Decorator](#decorator)
- [dataclass](#dataclass)
- [Dict of comprehension](#dict_of_comprehension)
- [Difference between pip and poetry](#difference_between_pip_and_poetry)
- [Difference between threads, async, and multiprocessing](#difference_between_threads_async_and_multiprocessing)
- [Exception Handling](#exception_handling)
- [Fixtures](#fixtures)
- [Garbage collector](#garbage_collector)
- [Generators](#generators)
- [httpx](#httpx)
- [Hashable objects](#hashable_objects)
- [Inherit from base types in Python](#inherit_from_base_types_in_python)
- [Iterators](#iterators)
- [List of comprehension](#list_of_comprehension)
- [@lru_cache](#lru_cache)
- [Multiprocessing](#multiprocessing)
- [Mutable and immutable objects](#mutable_and_immutable_objects)
- [MRO](#mro)
- [Overloading](#overloding)
- [@property](#property) 
- [Protected and Private method in class](#protected_and_private_method_in_class)
- [Protocol](#protocol)
- [Set and dict useful operations](#set_and_dict_useful_operations)
- [Slots](#slots)
- [Threads](#threads)
- [What data structure is under `list` and `dict`?](#what_data_structure_is_under_list_and_dict)
- [Why 0.1 + 0.2 is not equal to 0.3?](#why_01_02_is_not_equal_to_03)
- [@wraps](#wraps)
- [`zip`](#zip)

## .lock file <a name="lock_file"></a>
A .lock file has the exact versions of all dependencies to ensure consistent and repeatable package installations across environments. In contrast to `requirements.txt` or `pyproject.toml`, it also includes the exact versions of transitive dependencies.

## Abstraction in Python <a name="abstraction_in_python"></a>
Abstract classes are a blueprints for subclasses. Defining a common interface but leaving the actual implementation to the child classes.
Abstraction is a way to hide complex implementation details and show only the necessary features of an object. We can't instantiate abstract class. This will throw an error.
```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "Woof!"

animal = Animal()  # ❌ This will raise an error

dog = Dog()
print(dog.sound())  # Output: Woof!
```

## Asterisk in function definition <a name="asterisk_in_function_definition"></a>
It tells Python that any arguments that follow must be specified using keyword syntax:
```python
def func(*, a, b):
    pass

func(1, 2)  # raises TypeError:
func(a=1, b=2)  # this works
```

## `@classmethod` and `@staticmethod` <a name="classmethod_and_staticmethod"></a>
- `@classmethod` decorator operates and takes a class as an argument (`cls`). 
- `@staticmethod` don't need a `self` argument. 

## Code quality <a name="code_quality"></a>
Code quality tools available in Python:
- `ruff` - linter and code formatter (flake8, black and isort in one command)
- `black` - a code formatter that enforces a specific style. 
- `flake8` - code quality tool. Offers a broader range of checks compared to Black, covering both style and code quality concerns. 
- `isort` - sort imports alphabetically, and automatically separated into sections and by type. (can be compatible with black)
- `mypy` - type checker for Python
- `pydantic` - enforces type hints at runtime, and provides user-friendly errors when data is invalid. It offers features like data validation, input sanitization, serialization, and deserialization.

## Composition vs Inheritance <a name="composition_vs_inheritance"></a>
Composition is when one class __has__ another class. Composition gives more flexibility and avoids tight class coupling. Inheritance should be used when with a clear "is a" relationship. Use inheritance when you have a tight connection between classes.

## Context Managers <a name="context_managers"></a>
Context manager is an object that defines the behavior that should be performed before and after a block of code is executed. You use the context manager with the `with` keyword. To make your own context manager you create a class in it you define the methods `__entry__` and `__exit__` these are the methods that will be executed before and after executing the code located in the `with` block.

## Decorator <a name="decorator"></a>
A decorator is a function that wraps another function to add some functionality without modifying the original function's code.
```python
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")
    
say_hello() ## say_hello = my_decorator(say_hello)
            ## say_hello()
```

With additional parameter: 
```python
def repeat(n):
    def decorator(func):
        def wrapper():
            for _ in range(n):
                func()
        return wrapper
    return decorator

@repeat(3)
def say_hello():
    print("Hello!")

say_hello() ## say_hello = repeat(3)(say_hello)
            ## say_hello()
```

## dataclass <a name="dataclass"></a>
A dataclass is a decorator that automatically generates typical methods for a class mainly used to store data. Thanks to dataclass, you don’t have to manually write methods like:
- `__init__()` (constructor)
- `__repr__()` (readable text representation)
- `__eq__()` (object comparison)
- `__hash__()` (to be able to be a key in dict; only if flag frozen=True)

## Dict of comprehension <a name="dict_of_comprehension"></a>
Dict of comprehensions are generally faster than classic for loops because:
- They are internally optimized in C within the Python interpreter.
- For loops that use methods like append() or update() involve repeated function calls and introduce additional Python-level overhead, which makes them slower.

```python
{key: value for vars in iterable} e.g. {num: num*num for num in range (1,11)}
```

## Difference between pip and poetry <a name="difference_between_pip_and_poetry"></a>
`pip` - only installs packages.

`poetry` - manages all libraries by handling exact versions of packages and their dependencies, resolving dependency conflicts, and providing built-in virtual environment management.


## Difference between threads, async, and multiprocessing <a name="difference_between_threads_async_and_multiprocessing"></a>
- Threads - in Python create real system threads. We can't use the full power of threads in Python because of the GIL. While the program runs, the system decides when to preempt a thread and switch to another one. Therefore, when using threads, you should be careful about race condition.
- async/await - How it works? The tasks are added to the event loop which has three states: ready, waiting, and finished. event loop takes one task from the ready task list, runs it and when it hits "await" keyword it puts it back on the waiting list and then checks the list of the waiting tasks if they are still waiting and if not it puts it back to the ready or finished list. The "await" keyword gives the user full control over when to switch from one task to another. Unlike threads where the system decides about it. This will make "race condition" or "deadlock" errors occur much less frequently and are caused mainly by the programmer. I/O-bound tasks should use async/await or Threads.
- Multiprocessing - creates new Python instance so it has his own GIL. That alows to take full advantage of power of the processor. CPU-bound tasks should use multiprocessing.

## Exception Handling <a name="exception_handling"></a>
```python
try:
    # code that may cause exception
    x = int(input("Enter a number: "))
except ValueError:
    # code to run when exception occurs
    print("Invalid input")
else:
    # code to run when only when `try` is sucessed 
    print("The square of", x, "is", x ** 2)
finally:
    # code to run, regardless of whether an exception is raised or not
    print("Thank you for using the program.")
```

## Fixtures <a name="fixtures"></a>
Fixtures are functions, which will run before each test function to which it is applied. Fixtures are used to feed some data to the tests such as database connections, URLs to test and some sort of input data. 
```python
@pytest.fixture
def fixture_func():
   return "fixture test"

def test_fixture(fixture_func):
    assert fixture_func == "fixture test"
```

## Garbage collector <a name="garbage_collector"></a>
Python uses a reference counting algorithm to keep track of the number of references to an object. Every time a new reference to an object is created, the reference count for that object is incremented. Similarly, when a reference is deleted or goes out of scope, the reference count is decremented. When the reference count for an object reaches zero, it means that the object is no longer being used by the program, and it can be safely deallocated. At this point, the garbage collector is invoked to reclaim the memory used by the object.

Circular references is when two object are pointing to each other 
```python
class Node:
    def __init__(self):
        self.ref = None

a = Node()
b = Node()
a.ref = b
b.ref = a  # creates a cycle: a points to b, b points back to a

del a
del b 
# Even tho both objects are removed, the two Node objects still exist in memory, because of the circular reference. Python has a cycle detection mechanism that checks for unreachable cycles and removes them.
```

## Generators <a name="generators"></a>
A generator is a special type of iterator in Python that allows execution to be paused and resumed using the yield keyword. It only keeps track of its current state and what comes next — not the entire history. Generators are typically used for:

- Processing large amounts of data efficiently without loading everything into memory
- Generating infinite sequences without running out of resources
```python 
def fibonacci(n):
    a, b = 0, 1
    for i in range(n):
        yield a
        a, b = b, a + b
```
or you can use Generator Comprehension:
```python 
(i for i in range(100))
```

## httpx <a name="httpx"></a>
`httpx` is a modern HTTP client for Python (a successor to `requests`). It supports both synchronous and asynchronous requests, connection pooling, and HTTP/2.

## Hashable objects <a name="hashable_objects"></a>
Object in Python is hashable if it has the `__hash__()` method. Hashable objects are "faster" which means you will find a value in a tuple faster than in a list.

## Inherit from base types in Python <a name="inherit_from_base_types_in_python"></a>
Two main reasons why we shouldn't do that are:
- Overriding some in-build methods can cause in unexpected results
- In-build methods are usually implemented in C for performance reasons, and they have optimizations that are not available in Python code. Overriding them can casue an lost performance

## Iterators <a name="iterators"></a>
Iterators in Python are just objects that you can iterate at. The iterator remembers its current state. To create you own Iterator you need a class with two magic methods:
- `__iter__()` which returns the iterator object itself and it is used to initialize the iterator.
- `__next__()` which returns the next item from the iterator. It raises the `StopIteration` exception when there are no more items left to return.

Iterators are used to loop through a large amount of data because they remember only teh current state and the next item so it is memory-optimized. The downside of it is that you don't have access to previous or after elements.

## List of comprehension <a name="list_of_comprehension"></a>
List of comprehensions are generally faster than classic for loops because:
- They are internally optimized in C within the Python interpreter.
- For loops that use methods like append() or update() involve repeated function calls and introduce additional Python-level overhead, which makes them slower.

```python
[expression for item in list]
```
or
```python
[expression for item in list if expression else expression]
```

## @lru_cache <a name="lru_cache"></a>
Caches function results to speed up subsequent calls with the same arguments.

## Multiprocessing <a name="multiprocessing"></a>
Multiprocessing in python can be accesible using `multiprocessing` or `concurrent.futures` libraries. Both create new processes with their own GILs, but `concurrent.futures` provides a higher-order API which means that it should be easier to use in most cases.

## Mutable and immutable objects <a name="mutable_and_immutable_objects"></a>
Mutable objects are objects whose values can be changed after creation, while immutable objects are objects whose values cannot be changed after creation.
- immutable objects: `int`, `float`, `str`, `tuple`, `frozenset`, `bytes`
- mutable objects: `list`, `dict`, `set`, `bytearray`

So when you edit a string or number, Python underneath creates a new variable.

## MRO <a name="mro"></a>
Method Resolution Order - defines the order in which classes are searched when executing a method in multiple inheritance to ensure a consistent and predictable hierarchy. (left-to-right)
```python
class A:
    @staticmethod
    def func():
        print("test from A")


class B:
    @staticmethod
    def func():
        print("test from A")


class C(A, B):
    pass


print(C.__mro__) ## -> (<class '__main__.C'>, <class '__main__.A'>, <class '__main__.B'>, <class 'object'>)
```

## Overloading <a name="overloading"></a>
Python doesn't support function overloading in the traditional sense. If multiple functions with the same name are defined, only the last one will be used.

```python
def greet():
    print("Hello")


def greet(name):
    print(f"Hello, {name}")


greet("hubert") # -> Hello hubert
greet() # -> TypeError: greet() missing 1 required positional argument: 'name'
```
However, it's possible to mimic function overloading in Python using the following approaches:
- default arguments:
```python 
def greet(name="world"):
    print(f"Hello, {name}!")

greet()          # Hello, world!
greet("Alice")   # Hello, Alice!
```

- handling different argument types:
```python 
def add(a, b):
    if isinstance(a, str) or isinstance(b, str):
        return str(a) + str(b)
    return a + b

print(add(1, 2))       # 3
print(add("a", "b"))   # ab
```

- Using `functools.singledispatch`:
```python 
from functools import singledispatch

@singledispatch
def process(value):
    print("Generic case:", value)

@process.register(int)
def _(value):
    print("It's an integer:", value)

@process.register(str)
def _(value):
    print("It's a string:", value)

process(10)      # It's an integer: 10
process("abc")   # It's a string: abc
process([1, 2])  # Generic case: [1, 2]
```

## `@property` <a name="property"></a>
`@property` is a way to define a class attribute with custom getter, setter and deleter methods.
```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius

    @radius.setter
    def radius(self, value):
        self._radius = value

    @radius.deleter
    def radius(self):
        del self._radius
```

## Protected and Private method in class <a name="protected_and_private_method_in_class"></a>
- Protected (starts with one underscore) methods should be used only within a class or its subclasses. Not by the instance of a class/subclass. But using it won't throw an error. 
- Private (starts with two underscores) methods can be used only within a class. Trying to use it by the instance of a class or in the subclass will throw an error

## Protocol <a name="protocol"></a>
`typing.Protocol` is another method of providing abstraction, but unlike abstract classes, it does not require inheritance and offers greater flexibility than the traditional approach.

```python
from typing import Protocol

class SupportsClose(Protocol):
    def close(self) -> None:
        ...

class File:
    def close(self) -> None:
        print("File closed")

def close_resource(resource: SupportsClose) -> None:
    resource.close()

f = File()
close_resource(f)  # Works because File has a close() method
```

## Set and dict useful operations <a name="set_and_dict_useful_operations"></a>
```python 
a, b = {1, 2, 3}, {3, 4, 5, 6}
a & b # return intersection -> {3}
a | b # return union -> {1, 2, 3, 4, 5, 6}
a - b # return difference -> {1, 2}
a ^ b # XOR operation -> {1, 2, 4, 5, 6}

c, d = {'a': 1, 'c': 2}, {'a': 3, 'b': 4}
c | d # return union, right part is more important -> {'a': 3, 'c': 2, 'b': 4}
```

## Slots <a name="slots"></a>
Slots in Python is a special mechanism that is used to reduce memory of the objects and speed attribute access. This is because unlike regular classes where the attributes are based on a dictionary, attributes in the slots class have permanently allocated memory (slots class doesn't have `__dict__` and `__weakref__` methods). The downside of this solution is that we cannot dynamically add new attributes to the class.

```python
class Person:
    def __init__(self, name: str, address: str, email: str):
        self.name = name
        self.address = address
        self.email = email


class PersonSlots:
    __slots__ = "name", "address", "email"

    def __init__(self, name: str, address: str, email: str):
        self.name = name
        self.address = address
        self.email = email

person = Person()
person.age = "23" # this will work

person_slots = PersonSlots()
person_slots.age = "23" # this will rise AttributeError 
```


It is also worth mentioning that dataclass has the slost attribute set to false by default.


## Threads <a name="threads"></a>
Due to the existence of the GIL, Threads in Python are unable to take full advantage of multi-core processors. A bitcode can only be executed by one process that has the main thread. However, Threads are useful if we have input/output (I/O) operations, i.e. reading from files, other devices, or network sockets. For example, while waiting for a response from a request, the GIL is free to do other things.

## What data structure is under `list` and `dict`? <a name="what_data_structure_is_under_list_and_dict"></a>
- list - dynamic array
- dict - hash table

## Why 0.1 + 0.2 is not equal to 0.3? <a name="why_01_02_is_not_equal_to_03"></a>
This is because how floating point numbers works in most programming languages. To prevent this, we can use the `Decimal` class from the `decimal` library and set the precision (number of significant digits after the decimal point) to a specific value: `getcontext().prec = 4`

## @wraps <a name="wraps"></a>
Is a decorator available in the `functools` module that is used to preserve the original function's metadata when creating your own decorators (like `__name__` or `__doc__`).

```python
from functools import wraps

def decorator(fun):
    @wraps(fun)
    def wrapper(*args, **kwargs):
        print("Before function execution")
        return fun(*args, **kwargs)

    return wrapper

@decorator
def hello():
    """This functions says hello."""
    print("Hello!")

print(hello.__name__)  # outcome: Hello! 
print(hello.__doc__)  # outcome: This functions says hello.
# Without @wraps
# print(przywitaj.__name__)  # outcome: wrapper
# print(przywitaj.__doc__)   # outcome: None
```

## zip <a name="zip"></a>
The `zip(*iterables)` function takes iterables (can be zero or more), aggregates them in a tuple, and returns it:
```python
l1 = [1, 12, 3, 55, 5]
l2 = [6, 7, 8, 9, 10]
l3 = [2, 3, 4, 5, 12]

list(zip(l1, l2, l3)) # -> [(1, 6, 2), (12, 7, 3), (3, 8, 4), (55, 9, 5), (5, 10, 12)]

for x, y, z in zip(l1, l2, l3):
    print(x, y, z) # -> x=1, y=6, z=2 in first iteration 

# can use it also with list of comprehension
[min(x, y, z, ) for x, y, z in zip(l1, l2, l3)]
```

if one of list is shorter than rest zip will stop as soon as the shortest iterable is exhausted:
```python 
l1 = [1, 12, 3]
l2 = [6, 7, 8]
l3 = [2, 3]

list(zip(l1, l2, l3)) # -> [(1, 6, 2), (12, 7, 3)]
```

if you want to keep iterating until the longest iterable is exhausted and fill the missing values with a value (default=`None`), you can use the itertools.zip_longest():
```python 
import itertools
l1 = [1, 12, 3]
l2 = [6, 7, 8]
l3 = [2, 3]

list(itertools.zip_longest(l1, l2, l3, fillvalue=float("inf"))) # -> [(1, 6, 2), (12, 7, 3), (3, 8, inf)]
```
