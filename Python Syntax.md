# Python Syntax

Basic syntax rules and conventions in Python.

## Indentation

Python uses indentation to define code blocks (unlike braces in other languages).

```python
if 5 > 2:
    print("Five is greater than two!")  # Indented block
```

⚠️ Inconsistent indentation will cause errors.

## Comments

See [[Python Comments]] for detailed information.

```python
# This is a single-line comment
```

## Variables

See [[Python Variables]] for detailed information.

```python
x = 5
name = "Python"
```

## Case Sensitivity

Python is case-sensitive:
```python
Name = "John"
name = "Jane"  # Different variable
```

## Multiple Statements

Multiple statements on one line (not recommended):
```python
x = 5; y = 10; z = 15
```

## Line Continuation

```python
# Using backslash
total = 1 + 2 + 3 + \
        4 + 5 + 6

# Implicit (inside parentheses, brackets, braces)
total = (1 + 2 + 3 +
         4 + 5 + 6)
```

## Naming Conventions

- Variables and functions: `snake_case`
- Classes: `PascalCase`
- Constants: `UPPER_CASE`

---

**Related:** [[Python Comments]] | [[Python Variables]] | [[Python Basics]]
