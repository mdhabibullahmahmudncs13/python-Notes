# Python OOP Concepts

Core concepts of Object-Oriented Programming in Python.

**Deep Dive:** See [[Data Structures in Python/03 - Object-Oriented Programming|OOP in Data Structures]] for advanced patterns and real-world applications

## What is OOP?

Object-Oriented Programming is a paradigm that organizes code into objects containing data (attributes) and code (methods).

## Key Concepts

### Class
Blueprint for creating objects:
```python
class Dog:
    def __init__(self, name):
        self.name = name
```

### Object
Instance of a class:
```python
my_dog = Dog("Rex")
```

### Attributes
Data stored in an object:
```python
class Person:
    def __init__(self, name, age):
        self.name = name  # Instance attribute
        self.age = age
```

### Methods
Functions defined in a class:
```python
class Dog:
    def bark(self):
        print("Woof!")
```

## The Four Pillars

### 1. Encapsulation
Bundle data and methods:
```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private
    
    def deposit(self, amount):
        self.__balance += amount
    
    def get_balance(self):
        return self.__balance
```

### 2. Inheritance
Create new classes from existing ones:
```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"
```

### 3. Polymorphism
Same interface, different implementations:
```python
def make_sound(animal):
    print(animal.speak())

make_sound(Dog())  # Woof!
make_sound(Cat())  # Meow!
```

### 4. Abstraction
Hide complex details:
```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```

---

**Related:** [[Object-Oriented Programming]] | [[Python Classes and Objects]] | [[Python Inheritance]]
