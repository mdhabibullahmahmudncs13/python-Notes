# Python Polymorphism

Polymorphism allows objects of different types to be accessed through the same interface.

**Deep Dive:** See [[Data Structures in Python/03 - Object-Oriented Programming|OOP in Data Structures]] for duck typing and polymorphism in Python

## Function Polymorphism

```python
# len() works with different types
print(len("Hello"))        # 5
print(len([1, 2, 3]))      # 3
print(len({'a': 1, 'b': 2}))  # 2
```

## Class Polymorphism

```python
class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

class Bird:
    def speak(self):
        return "Chirp!"

def make_sound(animal):
    print(animal.speak())

dog = Dog()
cat = Cat()
bird = Bird()

make_sound(dog)   # Woof!
make_sound(cat)   # Meow!
make_sound(bird)  # Chirp!
```

## Polymorphism with Inheritance

```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

animals = [Dog(), Cat(), Dog()]
for animal in animals:
    print(animal.speak())
```

## Method Overloading

Python doesn't support traditional method overloading, but you can use default arguments:

```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c

calc = Calculator()
print(calc.add(5))        # 5
print(calc.add(5, 3))     # 8
print(calc.add(5, 3, 2))  # 10
```

## Operator Overloading

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        return Point(self.x + other.x, self.y + other.y)
    
    def __str__(self):
        return f"({self.x}, {self.y})"

p1 = Point(1, 2)
p2 = Point(3, 4)
p3 = p1 + p2
print(p3)  # (4, 6)
```

---

**Related:** [[Object-Oriented Programming]] | [[Python Inheritance]] | [[Python Classes and Objects]]
