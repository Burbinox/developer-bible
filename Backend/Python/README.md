# Python
- [List of comprehension](#list_of_comprehension)
- [Dict of comprehension](#dict_of_comprehension)
- [Context Managers](#context_managers)
- [Iterators](#iterators)
- [Generators](#generators)
- [Hashable objects](#hashable_objects)
- ["*" in function defintion ](#*_in_function_definition)
- [Mutable and immutable objects](#mutable_and_immutable_objects)
- [Protected and Private method in class](#protected_and_private_method_in_class)
## List of comprehension <a name="list_of_comprehension"></a>
``` python
[expression for item in list]
```
or
``` python
[expression for item in list if expression else expression]
```

## Dict of comprehension <a name="dict_of_comprehension"></a>
``` python
{key: value for vars in iterable} e.g. {num: num*num for num in range (1,11)}
```

## Context Managers <a name="context_managers"></a>
Context manager is an object that defines the behavior that should be performed before and after a block of code is executed. You use the context manager with the `with` keyword. To make your own context manager you create a class in it you define the methods `__entry__` and `__exit__` these are the methods that will be executed before and after executing the code located in the `with` block.

## Iterators <a name="iterators"></a>
Iterators in Python are just objects that you can iterate at. The iterator remembers its current state. To create you own Iterator you need a class with two magic methods:
- `__iter__()` which returns the iterator object itself and it is used to initialize the iterator.
- `__next__()` which returns the next item from the iterator. It raises the `StopIteration` exception when there are no more items left to return.

Iterators are used to loop through a large amount of data because they remember only teh current state and the next item so it is memory-optimized. The downside of it is that you don't have access to previous or after elements.

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

## "*" in function defintion <a name="*_in_function_definition"></a>
It tells Python that any arguments that follow must be specified using keyword syntax:
``` python
def func(*, a, b):
    pass

func(1, 2)  # raises TypeError:
func(a=1, b=2)  # this works
```

## Mutable and immutable objects <a name="mutable_and_immutable_objects"></a>
Mutable objects are objects whose values can be changed after creation, while immutable objects are objects whose values cannot be changed after creation.
- immutable objects: `int`, `float`, `str`, `tuple`, `frozenset`, `bytes`
- mutable objects: `list`, `dict`, `set`, `bytearray`

So when you edit a string or number, Python underneath creates a new variable.

## Protected and Private method in class <a name="protected_and_private_method_in_class"></a>
- Protected (starts with one underscore) methods should be used only within a class or its subclasses. Not by the instance of a class/subclass. But using it won't throw an error. 
- Private (starts with two underscores) methods can be used only within a class. Trying to use it by the instance of a class or in the subclass will throw an error