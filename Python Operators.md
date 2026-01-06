# Python Operators

Operators are used to perform operations on variables and values.

## Arithmetic Operators

```python
x = 10
y = 3

print(x + y)   # 13  Addition
print(x - y)   # 7   Subtraction
print(x * y)   # 30  Multiplication
print(x / y)   # 3.333... Division
print(x % y)   # 1   Modulus (remainder)
print(x ** y)  # 1000 Exponentiation
print(x // y)  # 3   Floor division
```

## Assignment Operators

```python
x = 5       # Assign
x += 3      # x = x + 3
x -= 3      # x = x - 3
x *= 3      # x = x * 3
x /= 3      # x = x / 3
x %= 3      # x = x % 3
x //= 3     # x = x // 3
x ** = 3    # x = x ** 3
x &= 3      # x = x & 3
x |= 3      # x = x | 3
x ^= 3      # x = x ^ 3
x >>= 3     # x = x >> 3
x <<= 3     # x = x << 3
x := 3      # Walrus operator (assignment expression)
```

## Comparison Operators

Return Boolean values:

```python
x = 5
y = 3

print(x == y)   # False  Equal
print(x != y)   # True   Not equal
print(x > y)    # True   Greater than
print(x < y)    # False  Less than
print(x >= y)   # True   Greater than or equal
print(x <= y)   # False  Less than or equal
```

## Logical Operators

```python
x = 5

# and - Returns True if both are True
print(x > 3 and x < 10)  # True

# or - Returns True if one is True
print(x > 3 or x < 4)    # True

# not - Reverse the result
print(not(x > 3 and x < 10))  # False
```

Truth tables:
```python
True and True    # True
True and False   # False
False and False  # False

True or True     # True
True or False    # True
False or False   # False

not True         # False
not False        # True
```

## Identity Operators

Check if objects are the same (same memory location):

```python
x = ["apple", "banana"]
y = ["apple", "banana"]
z = x

print(x is z)      # True (same object)
print(x is y)      # False (different objects)
print(x == y)      # True (same content)

print(x is not y)  # True
```

## Membership Operators

Check if a value is in a sequence:

```python
x = ["apple", "banana", "cherry"]

print("banana" in x)      # True
print("orange" not in x)  # True

# Works with strings too
text = "Hello World"
print("Hello" in text)    # True
print("Bye" not in text)  # True
```

## Bitwise Operators

Operate on binary representations:

```python
x = 10  # Binary: 1010
y = 4   # Binary: 0100

print(x & y)   # 0   AND
print(x | y)   # 14  OR
print(x ^ y)   # 14  XOR
print(~x)      # -11 NOT (inverts all bits)
print(x << 2)  # 40  Left shift
print(x >> 2)  # 2   Right shift
```

Bitwise operations:
```
  1010  (10)      1010  (10)      1010  (10)
& 0100  (4)    | 0100  (4)     ^ 0100  (4)
-------        -------         -------
  0000  (0)      1110  (14)     1110  (14)
```

## Operator Precedence

From highest to lowest:

1. `()` - Parentheses
2. `**` - Exponentiation
3. `+x`, `-x`, `~x` - Unary plus, minus, NOT
4. `*`, `/`, `//`, `%` - Multiplication, division, floor division, modulus
5. `+`, `-` - Addition, subtraction
6. `<<`, `>>` - Bitwise shifts
7. `&` - Bitwise AND
8. `^` - Bitwise XOR
9. `|` - Bitwise OR
10. `==`, `!=`, `>`, `>=`, `<`, `<=`, `is`, `is not`, `in`, `not in` - Comparisons
11. `not` - Logical NOT
12. `and` - Logical AND
13. `or` - Logical OR

```python
# Example
result = 10 + 5 * 2    # 20 (not 30)
result = (10 + 5) * 2  # 30
```

## Walrus Operator (:=)

Assignment expression (Python 3.8+):

```python
# Assign and use in one line
if (n := len([1, 2, 3])) > 2:
    print(f"List has {n} items")

# Useful in while loops
while (line := input("Enter: ")) != "quit":
    print(f"You entered: {line}")
```

---

**Related:** [[Python Numbers]] | [[Python Booleans]] | [[Python If Else]] | [[Python Basics]]
