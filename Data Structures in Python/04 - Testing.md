# Testing

← [[03 - Object-Oriented Programming]] | [[Data Structures in Python]] | Next: [[05 - Running Time Analysis]] →

## Why Testing Matters

Python is an **interpreted language** with:
- Great flexibility (like [[03 - Object-Oriented Programming#Duck Typing|duck typing]])
- Potential for runtime bugs
- No compile-time type checking

**Testing determines two things:**
1. Does the code work?
2. Does it still work after changes?

## Core Testing Principle

> [!important]
> **Test behavior, not implementation**

Test what the code is **supposed to do**, not how it does it.

## Writing Tests

### Simple Assertions

```python
class Doubler:
    def __init__(self, n):
        self._n = 2 * n
    
    def n(self):
        return self._n

if __name__ == '__main__':
    x = Doubler(5)
    assert(x.n() == 10)
    
    y = Doubler(-4)
    assert(y.n() == -8)
```

**Benefits of assertions over print:**
- Automatic verification (don't need to manually check output)
- No temptation to delete them
- Fail fast when expectations violated

> [!warning]
> **Never delete passing tests!** Code changes, and you want to know if changes break things.

### The `__name__` Guard

```python
if __name__ == '__main__':
    # Tests only run when executed directly
    # Not when imported as a module
```

## The OGAE Protocol

> [!tip]
> **OGAE: "Oh Good, An Error!"**

Every error is a favor - it reveals a problem in a safe environment.

Practice saying this with genuine enthusiasm when you encounter errors!

## Unit Testing with unittest

For serious programs, use proper **unit tests**:
- **Unit**: A single, indivisible test case
- Tests specific behavior of specific function
- Many tests, run all of them every time code changes

### Basic unittest Structure

```python
import unittest
from dayoftheweek import DayOfTheWeek

class TestDayOfTheWeek(unittest.TestCase):
    def testinitwithabbreviation(self):
        d = DayOfTheWeek('F')
        self.assertEquals(d.name(), 'Friday')
        
        d = DayOfTheWeek('Th')
        self.assertEquals(d.name(), 'Thursday')

unittest.main()
```

**Key points:**
- Import `unittest`
- Import code to test
- Create class extending `unittest.TestCase`
- Test methods **must** start with `test`
- Call `unittest.main()` to run tests

### Tests as Specification

> [!note]
> Unit tests often give the **clearest specification** of expected behavior.

Benefits:
- Executable documentation
- Always up-to-date (unlike comments)
- Shows how to use the code
- Verifies behavior actually works

Related: [[03 - Object-Oriented Programming#Encapsulation]] for understanding public interfaces

## Test-Driven Development (TDD)

### The Core Idea

> [!important]
> Write tests **before** writing code

### Why TDD?

Forces you to:
1. **Decide how to use the code** before writing it
2. **Write only needed code** - if no test needs it, don't write it

### Red-Green-Refactor

The TDD mantra:

1. **🔴 Red**: Write a test that fails (if it passes, either done or test is wrong)
2. **🟢 Green**: Write minimal code to make test pass
3. **♻️ Refactor**: Clean up code, remove duplication

> [!note]
> Red and Green refer to testing frameworks showing failed tests in red, passing tests in green.

### Refactoring

**Refactoring**: Cleaning up code, removing duplication

#### Example: Before Refactoring

```python
# Original with duplication:
avg1 = sum(L1)/len(L1)
avg2 = sum(L2)/len(L2)

# Updated with more duplication:
if len(L1) == 0:
    avg1 = 0
else:
    avg1 = sum(L1) / len(L1)

if len(L2) == 0:
    avg2 = 0
else:
    avg2 = sum(L2) / len(L2)
```

#### After Refactoring

```python
def avg(L):
    if len(L) == 0:
        return 0
    else:
        return sum(L) / len(L)

avg1 = avg(L1)
avg2 = avg(L2)
```

**Benefits:**
- Logic in one place
- Easier to read
- Easier to modify
- Fewer bugs

> [!important]
> If you duplicate code with a bug, now you have **two bugs**.
> If you find the bug, you must remember to fix it in **both places**.

Related: [[03 - Object-Oriented Programming#Avoiding Duplication (DRY)|DRY Principle]]

## What to Test

### Step Away from the Computer

Before writing tests, think:
- What **should** happen when I run this code?
- How do I **want** to use this code?

### Testing Strategy

1. **Test correct usage:**
   - Write tests that use code correctly
   - Verify expected behavior

2. **Test incorrect usage:**
   - Use code incorrectly
   - Test code fails gracefully
   - Check for clear error messages

3. **Test edge cases:**
   - Empty inputs
   - Maximum/minimum values
   - Boundary conditions

4. **Test typical cases:**
   - Common use patterns
   - Representative examples

## Testing and Object-Oriented Design

### Classes and Interfaces

In [[03 - Object-Oriented Programming|OOP]], we:
- Divide code into **classes** (nouns)
- Define **methods** (verbs)
- Create **public interface** to each class

### Writing Tests for OOP

**Identify expectations:**
- "If I call this method with these parameters, then this will happen"
- Express as unit tests

**Test each class individually:**
- Assume each class works correctly
- Reduces what you need to think about
- When composing classes, errors likely in new code

### Benefits of Thorough Testing

> [!warning]
> It may seem like wasted time, but skipping tests costs more time later!

**Without tests:**
- Unexpected behavior could be anywhere
- Debugging grinds to a halt
- Hours wasted searching for bugs

**With tests:**
- Errors isolated quickly
- Confidence in existing code
- Faster overall development

> [!tip]
> **When debugging fails:**
> 1. Stop
> 2. Pick one piece
> 3. Test it
> 4. Repeat
> 
> Being careful and systematic takes **less time overall**.
> **It is faster to go slow.**

## Testing Checklist

- [ ] Tests written before code (TDD)
- [ ] Each test has single, clear purpose
- [ ] All public methods tested
- [ ] Edge cases covered
- [ ] Error cases tested
- [ ] Tests run automatically
- [ ] All tests passing
- [ ] Code refactored after tests pass

## Related Topics

- [[03 - Object-Oriented Programming]] - OOP concepts to test
- [[05 - Running Time Analysis]] - Performance testing
- [[02 - Basic Python#Try Blocks]] - Exception handling in tests

---

*Test behavior, not implementation. Write tests first. Go slow to go fast.*
