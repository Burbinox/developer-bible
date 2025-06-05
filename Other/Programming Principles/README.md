# Programming Principles
- [Design patterns](#design_patterns)
- [DRY - Don't Repeat Yourself](#dry)
- [Functional Programming](#functional_programming)
- [KISS - Keep It Stupid, Simple](#kiss)
- [Monolith vs microservices](#monolith_vs_microservices)
- [Object-Oriented Programming](#oop)
- [Race condition in a REST API](#race_condition_in_a_rest_api)
- [SOLID](#solid)
- [YAGNI - You Ain't Gonna Need It](#yagni)

## Design patterns <a name="design_patterns"></a>
### Singletone 
Ensures that a class has only one instance. This is useful, for example, in managing a database connection where we don't want to create multiple connections.

### Decorator
It allows you to dynamically add new functionality to objects without changing their class. Very useful for extending the behavior of objects in a flexible way.

### Observer
Defines a mechanism for notifying multiple objects (observers) about changes in the state of another object (the observed one). Similar to pub/sub system.

```python
class WeatherStation:
    def __init__(self):
        self._observers = []
        self._temperature = None

    def attach(self, observer):
        self._observers.append(observer)

    def detach(self, observer):
        self._observers.remove(observer)

    def notify(self):
        for observer in self._observers:
            observer.update(self._temperature)

    def set_temperature(self, temperature):
        print(f"WeatherStation: Temperatura zmieniona na {temperature}°C")
        self._temperature = temperature
        self.notify()


class DisplayDevice:
    @staticmethod
    def update(temperature):
        print(f"Wyświetlacz: Aktualna temperatura to {temperature}°C")


class MobileApp:
    @staticmethod
    def update(temperature):
        print(f"Aplikacja mobilna: Powiadomienie - temperatura wynosi {temperature}°C")


weather_station = WeatherStation()

display = DisplayDevice()
app = MobileApp()

weather_station.attach(display)
weather_station.attach(app)

weather_station.set_temperature(25)
weather_station.set_temperature(30)
```

## DRY - Don't Repeat Yourself <a name="dry"></a>
Code should not be unnecessarily duplicated or repeated.

## Functional Programming <a name="functional_programming"></a>
Functional programming is based on pure functions, those that for the same input data will always give the same output data. It has no side effects which means it doesn't change the global variables. It also bases on the immutability of variables. Instead, new values are created as needed. This all together leads to code that is easier to understand, test, and debug.

## KISS - Keep It Stupid, Simple <a name="kiss"></a>
Code should be kept as simple and straightforward as possible

## Monolith vs microservices <a name="monolith_vs_microservices"></a>
Use monolith when:
- you have real-time systems where time is critical
- you need to transfer large amounts of data within the system (to avoid the overhead of network communication)

## Race condition in a REST API <a name="race_condition_in_a_rest_api"></a>
To prevent race conditions in REST API you can do the following things:
- Locking - ensure that only one request can access a critical section of code or a resource at a time.
- Versioning - system where each resource has a version number, and clients must include the current version number when making updates. If the version has changed since the client read the resource, the update is rejected.
- Transactions
- Idempotent System - making the same request multiple times produces the same result as making it once.

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

``` python 
class WorkerInterface:
    def work(self):
        pass

    def eat(self):
        pass

class Robot(WorkerInterface):
    def work(self):
        print("Robot is working")

    def eat(self):
        raise Exception("Robots don't eat")  # ❌ Violating ISP 
```

``` python 
class Workable:
    def work(self):
        pass

class Eatable:
    def eat(self):
        pass

class Human(Workable, Eatable):
    def work(self):
        print("Human is working")

    def eat(self):
        print("Human is eating")

class Robot(Workable):
    def work(self):
        print("Robot is working")  # ✅ Correct 

```

- **D**ependency Inversion Principle  - Abstractions should not depend upon details. Details should depend upon abstractions. (The implementation should change more often than the abstraction. The abstraction should not have unnecessary details, but only provide an interface).

``` python
class MySQLDatabase:
    def connect(self):
        print("Connecting to MySQL...")

class UserService:
    def __init__(self):
        self.db = MySQLDatabase()  # ❌ Direct dependency -> Violating DIP

    def get_user(self):
        self.db.connect()
        print("Getting user")

```

``` python
class Database:
    def connect(self):
        pass

class MySQLDatabase(Database):
    def connect(self):
        print("Connecting to MySQL...")

class UserService:
    def __init__(self, db: Database):
        self.db = db  # ✅ Depends on abstraction 

    def get_user(self):
        self.db.connect()
        print("Getting user")

```

## YAGNI - You Ain't Gonna Need It <a name="yagni"></a>
Developers should only implement features or functionality when it is necessary to meet the current requirements or solve a current problem.