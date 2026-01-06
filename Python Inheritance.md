# Python Inheritance

Inheritance allows a class to inherit attributes and methods from another class.
**Deep Dive:** See [[Data Structures in Python/03 - Object-Oriented Programming|OOP in Data Structures]] for inheritance vs composition and the "is a" relationship
## Basic Inheritance

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return f"{self.name} says Woof!"

class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow!"

dog = Dog("Rex")
print(dog.speak())  # Rex says Woof!
```

## super() Function

Access parent class methods:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Student(Person):
    def __init__(self, name, age, student_id):
        super().__init__(name, age)
        self.student_id = student_id

student = Student("Alice", 20, "S123")
```

## Method Overriding

```python
class Animal:
    def make_sound(self):
        return "Some sound"

class Dog(Animal):
    def make_sound(self):
        return "Woof!"

dog = Dog()
print(dog.make_sound())  # Woof!
```

## Multiple Inheritance

```python
class Father:
    def skills(self):
        print("Gardening")

class Mother:
    def skills(self):
        print("Cooking")

class Child(Father, Mother):
    pass

child = Child()
child.skills()  # Gardening (first parent)
```

## isinstance() and issubclass()

```python
class Animal:
    pass

class Dog(Animal):
    pass

dog = Dog()
print(isinstance(dog, Dog))     # True
print(isinstance(dog, Animal))  # True
print(issubclass(Dog, Animal))  # True
```

---

**Related:** [[Object-Oriented Programming]] | [[Python Classes and Objects]] | [[Python Polymorphism]]
