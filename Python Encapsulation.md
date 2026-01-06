# Python Encapsulation

Encapsulation restricts direct access to an object's data and methods.

**Deep Dive:** See [[Data Structures in Python/03 - Object-Oriented Programming|OOP in Data Structures]] for public interfaces and encapsulation principles

## Public, Protected, Private

```python
class Person:
    def __init__(self, name, age):
        self.name = name           # Public
        self._age = age            # Protected (convention)
        self.__salary = 50000      # Private (name mangling)
```

## Public Members

Accessible from anywhere:

```python
class Car:
    def __init__(self, brand):
        self.brand = brand  # Public

car = Car("Toyota")
print(car.brand)  # Toyota
car.brand = "Honda"
```

## Protected Members (_single_underscore)

Convention for internal use:

```python
class Person:
    def __init__(self, name, age):
        self._age = age  # Protected
    
    def get_age(self):
        return self._age

person = Person("Alice", 25)
print(person._age)  # Works but not recommended
```

## Private Members (__double_underscore)

Name mangling makes it harder to access:

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # Private
    
    def deposit(self, amount):
        self.__balance += amount
    
    def get_balance(self):
        return self.__balance

account = BankAccount(1000)
# print(account.__balance)  # AttributeError
print(account.get_balance())  # 1000

# Still accessible via name mangling (not recommended)
print(account._BankAccount__balance)  # 1000
```

## Property Decorators

Controlled access to attributes:

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = celsius
    
    @property
    def celsius(self):
        return self._celsius
    
    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Temperature below absolute zero")
        self._celsius = value
    
    @property
    def fahrenheit(self):
        return self._celsius * 9/5 + 32

temp = Temperature(25)
print(temp.celsius)     # 25
print(temp.fahrenheit)  # 77.0
temp.celsius = 30
```

## Getters and Setters

```python
class Person:
    def __init__(self, name):
        self.__name = name
    
    def get_name(self):
        return self.__name
    
    def set_name(self, name):
        if name:
            self.__name = name

person = Person("Alice")
print(person.get_name())
person.set_name("Bob")
```

---

**Related:** [[Object-Oriented Programming]] | [[Python Classes and Objects]] | [[Python Decorators]]
