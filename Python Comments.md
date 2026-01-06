# Python Comments

Comments are used to explain code and make it more readable. Python ignores comments during execution.

## Single-Line Comments

Start with `#`:

```python
# This is a comment
print("Hello, World!")  # This is also a comment
```

## Multi-Line Comments

Python doesn't have a specific multi-line comment syntax. Use multiple `#` or a multi-line string:

### Multiple Hash Symbols
```python
# This is a comment
# written across
# multiple lines
```

### Multi-Line Strings (Docstrings)
```python
"""
This is a multi-line comment
or docstring.
Used for documentation.
"""

'''
You can also use single quotes
for multi-line strings.
'''
```

## Docstrings

Special comments for documenting functions, classes, and modules:

```python
def my_function():
    """
    This function does something.
    
    Args:
        None
    
    Returns:
        None
    """
    pass
```

## Best Practices

- Write clear, concise comments
- Explain "why", not "what" (code shows what)
- Keep comments up-to-date
- Avoid obvious comments

```python
# Good comment
# Calculate compound interest for investment planning
interest = principal * rate * time

# Bad comment
# Set x to 5
x = 5
```

---

**Related:** [[Python Syntax]] | [[Python Functions]] | [[Python Basics]]
