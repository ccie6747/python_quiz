# Top 20 Python Interview Examples

Concise reference for common Python interview topics.

---

## 1. Shebang & Script Execution

```python
#!/usr/bin/env python3
# Makes script executable: chmod +x script.py && ./script.py

print("Hello from executable script")
```

---

## 2. The `__main__` Guard

```python
#!/usr/bin/env python3

def main():
    print("This runs only when script is executed directly")

if __name__ == "__main__":
    main()  # Won't run if this file is imported as a module
```

---

## 3. Variables & Data Types

```python
# Python is dynamically typed
name = "Alice"        # str
age = 30              # int
salary = 75000.50     # float
is_active = True      # bool
nothing = None        # NoneType

# Type checking
print(type(name))     # <class 'str'>
print(isinstance(age, int))  # True
```

---

## 4. Basic Function Definition

```python
def greet(name, greeting="Hello"):
    """Docstring: Returns a greeting message."""
    return f"{greeting}, {name}!"

# Calling the function
print(greet("Bob"))              # Hello, Bob!
print(greet("Bob", "Hi"))        # Hi, Bob!
print(greet(greeting="Hey", name="Bob"))  # Keyword args
```

---

## 5. *args and **kwargs

```python
def flexible_func(*args, **kwargs):
    """*args = tuple of positional args, **kwargs = dict of keyword args"""
    print(f"args: {args}")
    print(f"kwargs: {kwargs}")

flexible_func(1, 2, 3, name="Alice", age=30)
# args: (1, 2, 3)
# kwargs: {'name': 'Alice', 'age': 30}
```

---

## 6. Nested Functions & Closures

```python
def outer(x):
    """Outer function defines a variable"""
    def inner(y):
        """Inner function captures 'x' from enclosing scope"""
        return x + y
    return inner  # Return the inner function

add_five = outer(5)  # x=5 is "closed over"
print(add_five(3))   # 8 (5 + 3)
```

---

## 7. Lambda Functions

```python
# Anonymous single-expression functions
square = lambda x: x ** 2
add = lambda a, b: a + b

print(square(4))     # 16
print(add(2, 3))     # 5

# Common use: sorting
users = [("alice", 30), ("bob", 25)]
sorted_users = sorted(users, key=lambda u: u[1])  # Sort by age
```

---

## 8. For Loops

```python
# Iterating over a list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# Using range()
for i in range(5):       # 0, 1, 2, 3, 4
    print(i)

# Enumerate gives index + value
for idx, fruit in enumerate(fruits):
    print(f"{idx}: {fruit}")

# Loop with else (runs if no break)
for n in range(2, 5):
    if n == 10:
        break
else:
    print("Loop completed without break")
```

---

## 9. While Loops

```python
count = 0
while count < 3:
    print(f"Count: {count}")
    count += 1

# break and continue
n = 0
while True:
    n += 1
    if n == 2:
        continue  # Skip rest of loop body
    if n > 4:
        break     # Exit loop
    print(n)      # Prints 1, 3, 4
```

---

## 10. List Comprehensions

```python
# Basic: [expression for item in iterable]
squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]

# With condition
evens = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]

# With if-else (expression must come first)
labels = ["even" if x % 2 == 0 else "odd" for x in range(4)]
# ['even', 'odd', 'even', 'odd']

# Nested loops
matrix = [[1, 2], [3, 4]]
flat = [num for row in matrix for num in row]  # [1, 2, 3, 4]
```

---

## 11. Dictionary Comprehensions

```python
# Basic: {key: value for item in iterable}
squares = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# From two lists
keys = ["a", "b", "c"]
vals = [1, 2, 3]
combined = {k: v for k, v in zip(keys, vals)}  # {'a': 1, 'b': 2, 'c': 3}

# With condition
even_sq = {x: x**2 for x in range(10) if x % 2 == 0}
# {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}

# Inverting a dictionary
original = {"a": 1, "b": 2}
inverted = {v: k for k, v in original.items()}  # {1: 'a', 2: 'b'}
```

---

## 12. Classes & self Reference

```python
class Dog:
    """A simple class representing a dog."""

    species = "Canis familiaris"  # Class attribute (shared)

    def __init__(self, name, age):
        """Constructor: 'self' refers to the instance being created."""
        self.name = name  # Instance attribute
        self.age = age

    def bark(self):
        """Instance method: 'self' gives access to instance data."""
        return f"{self.name} says woof!"

    def get_info(self):
        return f"{self.name} is {self.age} years old"

# Creating and using instances
buddy = Dog("Buddy", 5)
print(buddy.bark())        # Buddy says woof!
print(buddy.get_info())    # Buddy is 5 years old
print(Dog.species)         # Canis familiaris
```

---

## 13. Class Inheritance

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        raise NotImplementedError("Subclass must implement")

class Cat(Animal):
    def speak(self):
        return f"{self.name} says meow!"

class Dog(Animal):
    def speak(self):
        return f"{self.name} says woof!"

# Polymorphism in action
animals = [Cat("Whiskers"), Dog("Rex")]
for animal in animals:
    print(animal.speak())
# Whiskers says meow!
# Rex says woof!
```

---

## 14. Importing Packages

```python
# Import entire module
import math
print(math.sqrt(16))      # 4.0
print(math.pi)            # 3.14159...

# Import specific items
from math import sqrt, pi
print(sqrt(25))           # 5.0

# Import with alias
import math as m
print(m.floor(3.7))       # 3

# Import all (avoid in production)
from math import *
```

---

## 15. Working with time Module

```python
import time

# Current timestamp (seconds since epoch)
print(time.time())        # 1702656000.123456

# Sleep/pause execution
print("Start")
time.sleep(1)             # Pause for 1 second
print("End")

# Formatted time
print(time.strftime("%Y-%m-%d %H:%M:%S"))  # 2024-12-15 10:30:00

# Measure execution time
start = time.time()
sum([i**2 for i in range(10000)])
elapsed = time.time() - start
print(f"Took {elapsed:.4f} seconds")
```

---

## 16. Math Operations

```python
import math

# Basic operations
print(abs(-5))            # 5
print(pow(2, 3))          # 8 (2^3)
print(round(3.7))         # 4
print(divmod(17, 5))      # (3, 2) -> (quotient, remainder)

# Math module functions
print(math.ceil(4.2))     # 5 (round up)
print(math.floor(4.8))    # 4 (round down)
print(math.sqrt(49))      # 7.0
print(math.factorial(5))  # 120
print(math.gcd(48, 18))   # 6 (greatest common divisor)
print(math.log(100, 10))  # 2.0 (log base 10)
```

---

## 17. Exception Handling

```python
def divide(a, b):
    try:
        result = a / b
    except ZeroDivisionError:
        return "Cannot divide by zero"
    except TypeError as e:
        return f"Type error: {e}"
    else:
        # Runs if no exception occurred
        return result
    finally:
        # Always runs (cleanup)
        print("Division attempted")

print(divide(10, 2))   # 5.0
print(divide(10, 0))   # Cannot divide by zero

# Raising exceptions
def validate_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    return age
```

---

## 18. File I/O

```python
# Writing to a file
with open("example.txt", "w") as f:
    f.write("Hello, World!\n")
    f.write("Second line\n")

# Reading entire file
with open("example.txt", "r") as f:
    content = f.read()
    print(content)

# Reading line by line
with open("example.txt", "r") as f:
    for line in f:
        print(line.strip())  # strip() removes newline

# Appending to file
with open("example.txt", "a") as f:
    f.write("Appended line\n")

# 'with' statement auto-closes file (context manager)
```

---

## 19. Decorators

```python
import time

def timer(func):
    """Decorator that measures function execution time."""
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} took {end - start:.4f}s")
        return result
    return wrapper

@timer  # Equivalent to: slow_function = timer(slow_function)
def slow_function():
    time.sleep(0.5)
    return "Done"

slow_function()  # Prints: slow_function took 0.50xxs
```

---

## 20. Common Data Structure Operations

```python
# LIST operations
lst = [1, 2, 3]
lst.append(4)          # [1, 2, 3, 4]
lst.insert(0, 0)       # [0, 1, 2, 3, 4]
lst.pop()              # Returns 4, lst = [0, 1, 2, 3]
lst.remove(2)          # [0, 1, 3]
lst.extend([4, 5])     # [0, 1, 3, 4, 5]
print(lst[::-1])       # [5, 4, 3, 1, 0] (reverse)

# DICTIONARY operations
d = {"a": 1, "b": 2}
d["c"] = 3             # Add key
d.get("x", "default")  # Safe access with default
d.keys()               # dict_keys(['a', 'b', 'c'])
d.values()             # dict_values([1, 2, 3])
d.items()              # dict_items([('a', 1), ...])
d.pop("a")             # Remove and return value

# SET operations
s = {1, 2, 3}
s.add(4)               # {1, 2, 3, 4}
s.discard(2)           # {1, 3, 4}
s1 = {1, 2, 3}
s2 = {2, 3, 4}
print(s1 & s2)         # {2, 3} intersection
print(s1 | s2)         # {1, 2, 3, 4} union
print(s1 - s2)         # {1} difference
```

---

## Quick Reference Table

| Topic | Key Concept |
|-------|-------------|
| Shebang | `#!/usr/bin/env python3` |
| Main guard | `if __name__ == "__main__":` |
| Function | `def func(arg):` |
| Lambda | `lambda x: x * 2` |
| List comp | `[x for x in items if cond]` |
| Dict comp | `{k: v for k, v in items}` |
| Class | `class Name:` with `self` |
| Inheritance | `class Child(Parent):` |
| Import | `import mod` / `from mod import x` |
| Exception | `try/except/else/finally` |
| Decorator | `@decorator` above function |
| Context mgr | `with open() as f:` |

---

*Created for Python interview preparation*
