# Programming Principles
- [DRY - Don't Repeat Yourself](#dry)
- [Functional Programming](#functional_programming)
- [KISS - Keep It Stupid, Simple](#kiss)
- [Object-Oriented Programming](#oop)
- [SOLID](#solid)
- [YAGNI - You Ain't Gonna Need It](#yagni)

## DRY - Don't Repeat Yourself <a name="dry"></a>
Code should not be unnecessarily duplicated or repeated.

## Functional Programming <a name="functional_programming"></a>
Functional programming is based on pure functions, those that for the same input data will always give the same output data. It has no side effects which means it doesn't change the global variables. It also bases on the immutability of variables. Instead, new values are created as needed. This all together leads to code that is easier to understand, test, and debug.

## KISS - Keep It Stupid, Simple <a name="kiss"></a>
Code should be kept as simple and straightforward as possible

## Object-Oriented Programming <a name="oop"></a>
Object-Oriented Programming (OOP) is a programming paradigm that uses objects, which are made up of attributes (data) and methods (behaviors), to represent and manipulate data. OOP principles: 
- Encapsulation - merges data and methods together, and hides the implementation details of a class from the outside world Encapsulation helps to protect the internal state of an object from accidental modification by providing methods to change class fields from the outside in control manner.
- Inheritance - this principle is about creating a new class that inherits the attributes and methods of an existing class, and then adding or modifying those attributes and methods as needed. 
- Polymorphism - allows you to access objects of different types through the same interface, and to use the same method to invoke different behaviors depending on the actual type of the object.
- Abstraction - the process of hiding complex implementation details and exposing only the necessary information to the user. It allows users to work with a simplified and easy-to-use interface, without having to know the specific implementation details.

## SOLID <a name="solid"></a>
**SOLID** is a set of five object-oriented design principles. **SOLID** is an acronym that groups five core principles that apply to object-oriented design. These principles are the following:
- **S**ingle Responsibility Principle - A class should have only one reason to change (class should have onlue one responsibility). Example:
``` python
from pathlib import Path
from zipfile import ZipFile

class FileManager:
    def __init__(self, filename):
        self.path = Path(filename)

    def read(self, encoding="utf-8"):
        return self.path.read_text(encoding)

    def write(self, data, encoding="utf-8"):
        self.path.write_text(data, encoding)

    def compress(self):
        with ZipFile(self.path.with_suffix(".zip"), mode="w") as archive:
            archive.write(self.path)

    def decompress(self):
        with ZipFile(self.path.with_suffix(".zip"), mode="r") as archive:
            archive.extractall()
```
In this example, your FileManager class has two different responsibilities. It uses the .read() and .write() methods to manage the file. It also deals with ZIP archives by providing the .compress() and .decompress() methods. Correct version should be:

``` python
from pathlib import Path
from zipfile import ZipFile

class FileManager:
    def __init__(self, filename):
        self.path = Path(filename)

    def read(self, encoding="utf-8"):
        return self.path.read_text(encoding)

    def write(self, data, encoding="utf-8"):
        self.path.write_text(data, encoding)

class ZipFileManager:
    def __init__(self, filename):
        self.path = Path(filename)

    def compress(self):
        with ZipFile(self.path.with_suffix(".zip"), mode="w") as archive:
            archive.write(self.path)

    def decompress(self):
        with ZipFile(self.path.with_suffix(".zip"), mode="r") as archive:
            archive.extractall()
```
- **O**pen-closed Principle - Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. (code should be open for extension. So we should be able to extend the existing code with new functionality, but closed for modification we shouldn't need to modify the original code, in order to do that). Example:

``` python
from math import pi

class Shape:
    def __init__(self, shape_type, **kwargs):
        self.shape_type = shape_type
        if self.shape_type == "rectangle":
            self.width = kwargs["width"]
            self.height = kwargs["height"]
        elif self.shape_type == "circle":
            self.radius = kwargs["radius"]

    def calculate_area(self):
        if self.shape_type == "rectangle":
            return self.width * self.height
        elif self.shape_type == "circle":
            return pi * self.radius**2
```
In this example, if you want to add a new shape you need to modify the current class. Correct version should be:

``` python
from abc import ABC, abstractmethod
from math import pi

class Shape(ABC):
    def __init__(self, shape_type):
        self.shape_type = shape_type

    @abstractmethod
    def calculate_area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        super().__init__("circle")
        self.radius = radius

    def calculate_area(self):
        return pi * self.radius**2

class Rectangle(Shape):
    def __init__(self, width, height):
        super().__init__("rectangle")
        self.width = width
        self.height = height

    def calculate_area(self):
        return self.width * self.height
```

- **L**iskov Substitution Principle - Subtypes must be substitutable for their base types. (objects of a child class should be able to replace objects of the base class without affecting the correctness of the program).

- **I**nterface Segregation Principle  - Clients should not be forced to depend upon methods that they do not use. Interfaces belong to clients, not to hierarchies. (overall it is better to have several specific interfaces instead of one general).

- **D**ependency Inversion Principle  - Abstractions should not depend upon details. Details should depend upon abstractions. (The implementation should change more often than the abstraction. The abstraction should not have unnecessary details, but only provide an interface).


## YAGNI - You Ain't Gonna Need It <a name="yagni"></a>
Developers should only implement features or functionality when it is necessary to meet the current requirements or solve a current problem.