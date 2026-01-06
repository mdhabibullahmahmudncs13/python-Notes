# Python Classes and Objects

Classes are blueprints for creating objects.

**Deep Dive:** See [[Data Structures in Python/03 - Object-Oriented Programming|OOP in Data Structures]] for detailed examples and design patterns

## Creating a Class

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def greet(self):
        print(f"Hello, I'm {self.name}")

# Create object
person1 = Person("Alice", 25)
person1.greet()  # Hello, I'm Alice
```

## The __init__ Method

Constructor method called when object is created:

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

dog = Dog("Rex", "Labrador")
print(dog.name)  # Rex
```

## The self Parameter

Refers to the current instance:

```python
class Counter:
    def __init__(self):
        self.count = 0
    
    def increment(self):
        self.count += 1
    
    def get_count(self):
        return self.count
```

## Class Attributes

Shared by all instances:

```python
class Dog:
    species = "Canis familiaris"  # Class attribute
    
    def __init__(self, name):
        self.name = name  # Instance attribute

dog1 = Dog("Rex")
dog2 = Dog("Max")
print(dog1.species)  # Canis familiaris
print(dog2.species)  # Canis familiaris
```

## Instance Methods

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius ** 2
    
    def circumference(self):
        return 2 * 3.14 * self.radius
```

## Class Methods

```python
class Person:
    count = 0
    
    def __init__(self, name):
        self.name = name
        Person.count += 1
    
    @classmethod
    def get_count(cls):
        return cls.count

person1 = Person("Alice")
person2 = Person("Bob")
print(Person.get_count())  # 2
```

## Static Methods

```python
class Math:
    @staticmethod
    def add(x, y):
        return x + y
    
    @staticmethod
    def multiply(x, y):
        return x * y

print(Math.add(5, 3))  # 8
```

## Properties

```python
class Person:
    def __init__(self, name):
        self._name = name
    
    @property
    def name(self):
        return self._name
    
    @name.setter
    def name(self, value):
        if value:
            self._name = value
    
    @name.deleter
    def name(self):
        del self._name

person = Person("Alice")
print(person.name)  # Alice (using getter)
person.name = "Bob"  # Using setter
```

## Magic Methods (Dunder Methods)

```python
class Book:
    def __init__(self, title, pages):
        self.title = title
        self.pages = pages
    
    def __str__(self):
        return f"{self.title} ({self.pages} pages)"
    
    def __len__(self):
        return self.pages
    
    def __eq__(self, other):
        return self.pages == other.pages

book = Book("Python Guide", 500)
print(book)  # Python Guide (500 pages)
print(len(book))  # 500
```

## Common Magic Methods

```python
__init__()    # Constructor
__str__()     # String representation
__repr__()    # Developer representation
__len__()     # Length
__eq__()      # Equality (==)
__lt__()      # Less than (<)
__add__()     # Addition (+)
__getitem__() # Indexing []
__call__()    # Make object callable
```

---

**Related:** [[Object-Oriented Programming]] | [[Python Inheritance]] | [[Python OOP Concepts]]
