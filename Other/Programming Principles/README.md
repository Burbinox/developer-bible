# Programming Principles
- [DRY - Don't Repeat Yourself](#dry)
- [Functional Programming](#functional_programming)
- [KISS - Keep It Stupid, Simple](#kiss)
- [Object-Oriented Programming](#oop)
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

## YAGNI - You Ain't Gonna Need It <a name="yagni"></a>
Developers should only implement features or functionality when it is necessary to meet the current requirements or solve a current problem.