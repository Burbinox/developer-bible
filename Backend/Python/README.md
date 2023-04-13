# Python
- ["*" in function defintion ](#*_in_function_definition)
- [@classmethod and @staticmethod](#classmethod_and_staticmethod)
- [Context Managers](#context_managers)
- [Dict of comprehension](#dict_of_comprehension)
- [Generators](#generators)
- [Hashable objects](#hashable_objects)
- [Iterators](#iterators)
- [List of comprehension](#list_of_comprehension)
- [Mutable and immutable objects](#mutable_and_immutable_objects)
- [@property](#property) 
- [Protected and Private method in class](#protected_and_private_method_in_class)

## "*" in function defintion <a name="*_in_function_definition"></a>
It tells Python that any arguments that follow must be specified using keyword syntax:
``` python
def func(*, a, b):
    pass

func(1, 2)  # raises TypeError:
func(a=1, b=2)  # this works
```

## `@classmethod` and `@staticmethod` <a name="classmethod_and_staticmethod"></a>
- `@classmethod` decorator operates and takes a class as an argument (`cls`). 
- `@staticmethod` don't need a `self` argument. 

## Context Managers <a name="context_managers"></a>
Context manager is an object that defines the behavior that should be performed before and after a block of code is executed. You use the context manager with the `with` keyword. To make your own context manager you create a class in it you define the methods `__entry__` and `__exit__` these are the methods that will be executed before and after executing the code located in the `with` block.

## Dict of comprehension <a name="dict_of_comprehension"></a>
``` python
{key: value for vars in iterable} e.g. {num: num*num for num in range (1,11)}
```

## Generators <a name="generators"></a>
Generator is a basicaly an Iterator but is much easier to create. 
``` python 
def fibonacci(n):
    a, b = 0, 1
    for i in range(n):
        yield a
        a, b = b, a + b
```
or you can use Generator Comprehension:
``` python 
(i for i in range(100))
```

## Hashable objects <a name="hashable_objects"></a>
Object in Python is hashable if it has the __hash__() method. Hashable objects are "faster" which means you will find a value in a tuple faster than in a list.

## Iterators <a name="iterators"></a>
Iterators in Python are just objects that you can iterate at. The iterator remembers its current state. To create you own Iterator you need a class with two magic methods:
- `__iter__()` which returns the iterator object itself and it is used to initialize the iterator.
- `__next__()` which returns the next item from the iterator. It raises the `StopIteration` exception when there are no more items left to return.

Iterators are used to loop through a large amount of data because they remember only teh current state and the next item so it is memory-optimized. The downside of it is that you don't have access to previous or after elements.

## List of comprehension <a name="list_of_comprehension"></a>
``` python
[expression for item in list]
```
or
``` python
[expression for item in list if expression else expression]
```

## Mutable and immutable objects <a name="mutable_and_immutable_objects"></a>
Mutable objects are objects whose values can be changed after creation, while immutable objects are objects whose values cannot be changed after creation.
- immutable objects: `int`, `float`, `str`, `tuple`, `frozenset`, `bytes`
- mutable objects: `list`, `dict`, `set`, `bytearray`

So when you edit a string or number, Python underneath creates a new variable.

## `@property` <a name="property"></a>
`@property` is a way to define a class attribute with custom getter, setter and deleter methods.
``` python
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
