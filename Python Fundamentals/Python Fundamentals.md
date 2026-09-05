# Python Language 

> A complete language-level guide to Python before Object-Oriented Programming.
>
> **Scope:** Python syntax, semantics, variables, data types, operators, control flow, functions, collections, comprehensions, iterators, generators, exceptions, files, modules, namespaces, copying, type hints, built-in functions, and Python-specific behavior.
>
> **Not covered:** DSA algorithms, competitive-programming techniques, classes, objects, inheritance, polymorphism, encapsulation, and other OOP concepts.

# 1. Python — The Language and Its Mental Model

## 1.1 What is Python?

Python is a high-level, general-purpose programming language designed with an emphasis on readability and developer productivity.

A Python program is written using statements and expressions that operate on objects.

The most important mental model to understand is:

> **In Python, variables are names that refer to objects.**

For example:

```python
x = 10
```

It is tempting to think:

```text
x = a box
10 = value stored inside the box
```

A better Python mental model is:

```text
object
  10
   ↑
   |
  x
```

`x` is a name referring to the integer object `10`.

This distinction becomes extremely important when working with mutable objects such as lists and dictionaries.

## 1.2 Python is dynamically typed

Python does not require you to declare the type of a variable before using it.

```python
x = 10
x = "hello"
x = [1, 2, 3]
```

The same name can refer to objects of different types at different times.

Conceptually:

```text
x → integer object

later

x → string object

later

x → list object
```

The object has a type. The name itself does not have a permanently fixed type.

This is one of the most important differences between Python's type model and languages where variables are normally declared with a fixed type.

## 1.3 Python is strongly typed

Dynamic typing does **not** mean that Python has no type rules.

Python still knows that:

```python
10
```

is an integer,

```python
"10"
```

is a string,

and

```python
[10]
```

is a list.

Therefore:

```python
10 + "20"
```

does not automatically combine the values.

Python raises:

```text
TypeError
```

You must explicitly convert when necessary:

```python
10 + int("20")
```

## 1.4 Interpreted, compiled, and executed

At a high level, Python source code is processed by the Python implementation before the instructions are executed.

The exact implementation details depend on the Python implementation, so avoid thinking of Python simply as "a language that is only interpreted."

A useful beginner mental model is:

```text
Python source code
       ↓
Python implementation processes it
       ↓
internal executable representation
       ↓
execution
```

The important point for programming is that you write Python source code, and the Python runtime executes it.

## 1.5 Statements and expressions

An expression produces a value.

```python
10 + 20
```

produces:

```text
30
```

Other examples:

```python
x
x + 5
len("hello")
[1, 2, 3]
```

A statement performs an action or controls execution.

Examples:

```python
x = 10

if x > 5:
    print(x)

for i in range(5):
    print(i)
```

Some Python constructs can behave as expressions:

```python
x = 10 if condition else 20
```

The important distinction is:

```text
Expression → produces a value

Statement → performs an operation / controls program execution
```

## 1.6 Everything important revolves around objects

Python has objects representing:

```text
integers
floating-point numbers
strings
lists
tuples
sets
dictionaries
functions
modules
files
etc.
```

Each object has characteristics such as:

```text
type
identity
value/state
```

For example:

```python
x = [1, 2, 3]
```

The list object has:

```text
type     → list
identity → identity of that particular list object
value    → [1, 2, 3]
```

Understanding objects becomes especially important for:

```text
mutability
assignment
aliasing
copying
function arguments
```

---

# 2. Python Syntax and Indentation

## 2.1 Indentation is part of Python syntax

Python uses indentation to represent blocks of code.

```python
if x > 0:
    print("positive")
    print("valid")
```

The indentation tells Python which statements belong to the `if` block.

There are no braces required to define the block.

Conceptually:

```text
if condition:
    statement
    statement
    statement
```

## 2.2 Colon

A colon generally introduces a block.

```python
if condition:
    ...
```

```python
for item in items:
    ...
```

```python
while condition:
    ...
```

```python
def function():
    ...
```

## 2.3 Indentation must be consistent

Correct:

```python
if x > 0:
    print(x)
    print("positive")
```

Incorrect:

```python
if x > 0:
    print(x)
      print("positive")
```

This can produce:

```text
IndentationError
```

Use a consistent indentation style. Four spaces per indentation level is the standard convention.

## 2.4 Comments

Single-line comment:

```python
# This is a comment
```

Python ignores the comment during execution.

Comments should explain why something is being done when the reason is not obvious.

## 2.5 Identifiers

Identifiers are names used for things such as:

```text
variables
functions
modules
etc.
```

Examples:

```python
age
student_name
total_count
calculate_sum
```

Identifiers cannot normally begin with a digit:

```python
2name
```

is invalid.

Underscore is allowed:

```python
_name
student_name
```

Python is case-sensitive:

```python
age
Age
AGE
```

are different names.

## 2.6 Keywords

Python reserves certain words for language syntax.

Examples include:

```text
if
else
elif
for
while
def
return
class
try
except
finally
import
from
as
in
is
and
or
not
True
False
None
```

You cannot use a keyword as an ordinary variable name.

---

# 3. Variables, Names, References, Identity and Assignment

## 3.1 What is a variable in Python?

A common beginner explanation is:

> A variable is a container that stores a value.

This explanation is convenient but incomplete for Python.

A more accurate model is:

> A variable name is a reference/name bound to an object.

Example:

```python
x = 10
```

Think:

```text
10 object
   ↑
   |
   x
```

## 3.2 Assignment does not mean "copy the value into a box"

Consider:

```python
a = [1, 2, 3]
b = a
```

A beginner may imagine:

```text
a → [1, 2, 3]
b → another [1, 2, 3]
```

But Python actually creates one list and two names referring to it:

```text
        ┌─────────────┐
a ─────→│ [1, 2, 3]   │
b ─────→│             │
        └─────────────┘
```

Therefore:

```python
b.append(4)
```

also changes what `a` sees:

```python
print(a)
```

Output:

```text
[1, 2, 3, 4]
```

## 3.3 Reassignment

Consider:

```python
x = 10
x = 20
```

The name `x` first refers to `10`, then it is rebound to `20`.

```text
x → 10

then

x → 20
```

The old object may eventually be removed if nothing references it.

## 3.4 Multiple assignment

Python allows:

```python
a = b = 10
```

Both names refer to the same object.

You can also write:

```python
a, b, c = 1, 2, 3
```

This performs unpacking.

## 3.5 Swapping values

Python supports direct swapping:

```python
a, b = b, a
```

Conceptually:

```text
evaluate right side
       ↓
create values to unpack
       ↓
assign to left-side names
```

You do not need a temporary variable.

## 3.6 Identity

Every object has an identity during its lifetime.

You can inspect identity using:

```python
id(obj)
```

Example:

```python
x = [1, 2]
y = x

print(id(x) == id(y))
```

Output:

```text
True
```

because both names refer to the same object.

## 3.7 `is` versus `==`

This is extremely important.

`==` asks:

> Do these objects have equal values?

`is` asks:

> Are these the same object?

Example:

```python
a = [1, 2]
b = [1, 2]
```

Usually:

```python
a == b
```

is:

```text
True
```

but:

```python
a is b
```

is:

```text
False
```

because they are two different list objects.

Use:

```python
==
```

for value equality.

Use:

```python
is
```

for identity checks.

A particularly important case is:

```python
x is None
```

rather than:

```python
x == None
```

## 3.8 Variable deletion

You can remove a name using:

```python
del x
```

This removes the binding of `x`.

It does not mean:

> "Destroy this object immediately."

If another name still refers to the object, the object can continue to exist.

---

# 4. Data Types and Type System

## 4.1 What is a data type?

A data type determines what kind of object something is and what operations are meaningful for it.

Examples:

```text
int
float
complex
bool
str
list
tuple
set
dict
bytes
bytearray
NoneType
```

You can inspect an object's type:

```python
type(x)
```

Example:

```python
x = 10
print(type(x))
```

## 4.2 Python does not require explicit variable declarations

You can write:

```python
x = 100
```

instead of specifying a type declaration first.

Python determines the type from the object assigned.

Later:

```python
x = "hello"
```

is also valid.

## 4.3 Checking types

Use:

```python
type(x)
```

for inspection.

Use:

```python
isinstance(x, int)
```

when you want to ask whether an object is an instance of a particular type.

Example:

```python
x = 10

print(isinstance(x, int))
```

Output:

```text
True
```

## 4.4 Type conversion

Python does not silently convert unrelated values merely because a conversion seems obvious.

Explicit conversion is common:

```python
int("123")
float("12.5")
str(123)
list("abc")
tuple([1, 2, 3])
set([1, 2, 2, 3])
```

The general idea is:

```text
original object
      ↓
conversion function
      ↓
new representation
```

## 4.5 Mutable and immutable types

This is one of the most important Python concepts.

### Immutable objects

Their value cannot be changed after creation.

Common immutable types include:

```text
int
float
bool
complex
str
tuple
frozenset
bytes
```

For example:

```python
s = "hello"
```

You cannot modify one character directly:

```python
s[0] = "H"
```

This raises:

```text
TypeError
```

Instead, create a new string:

```python
s = "H" + s[1:]
```

### Mutable objects

Their contents can be changed after creation.

Examples:

```text
list
dict
set
bytearray
```

Example:

```python
numbers = [1, 2, 3]
numbers[0] = 100
```

The same list object is modified.

## 4.6 Why mutability matters

Mutability affects:

```text
assignment
aliasing
function arguments
copying
data structures
default function arguments
```

Example:

```python
a = [1, 2]
b = a

b.append(3)
```

Now:

```text
a → [1, 2, 3]
b → [1, 2, 3]
```

because both names refer to the same mutable object.

---

# 5. Numeric Data Types

## 5.1 Integer — `int`

Integers represent whole numbers.

```python
x = 10
y = -50
z = 0
```

Python integers can grow beyond the size normally available in fixed-width integer types, limited primarily by available memory.

Therefore:

```python
x = 10 ** 100
```

is valid.

## 5.2 Floating-point — `float`

Used for numbers containing a fractional component.

```python
x = 10.5
y = 3.14
```

Floating-point numbers have finite precision.

Therefore calculations involving decimal values may sometimes produce surprising results.

For example:

```python
0.1 + 0.2
```

may not produce exactly:

```text
0.3
```

This is not a Python bug. It comes from the representation of many decimal fractions in binary floating-point arithmetic.

For exact decimal calculations, other tools such as `decimal` may be appropriate.

## 5.3 Complex numbers

Python has built-in complex numbers.

```python
z = 3 + 4j
```

The imaginary unit is represented by:

```text
j
```

You can access:

```python
z.real
z.imag
```

## 5.4 Boolean — `bool`

Boolean values are:

```python
True
False
```

They are used in conditions and logical operations.

Example:

```python
x = 10

print(x > 5)
```

Result:

```text
True
```

Python's boolean type has a special relationship with integers, but you should conceptually treat:

```text
True
False
```

as logical values rather than relying on integer-like behavior unnecessarily.

## 5.5 Arithmetic operators

```python
a + b
a - b
a * b
a / b
a // b
a % b
a ** b
```

### `/`

Normal division:

```python
7 / 2
```

produces:

```text
3.5
```

### `//`

Floor division:

```python
7 // 2
```

produces:

```text
3
```

Important:

> `//` means floor division, not simply "remove the decimal part."

For negative values:

```python
-7 // 2
```

produces:

```text
-4
```

because floor means moving toward negative infinity.

### `%`

Modulo/remainder:

```python
7 % 2
```

produces:

```text
1
```

### `**`

Exponentiation:

```python
2 ** 5
```

produces:

```text
32
```

## 5.6 Useful numeric functions

```python
abs(x)
pow(x, y)
round(x)
divmod(a, b)
min(...)
max(...)
sum(...)
```

Example:

```python
q, r = divmod(17, 5)
```

Conceptually:

```text
q → quotient
r → remainder
```

## 5.7 Numeric conversion

```python
int(10.9)
float(10)
complex(10)
bool(0)
```

Be careful:

```python
int(10.9)
```

does not perform mathematical rounding. It converts toward zero.

---

# 6. `None` and the Absence of a Value

## 6.1 What is `None`?

`None` represents the absence of a meaningful value.

```python
x = None
```

It is not:

```text
0
""
False
[]
```

Those are different objects/values.

## 6.2 `NoneType`

The type of `None` is:

```python
type(None)
```

which is:

```text
NoneType
```

## 6.3 Checking for `None`

Preferred:

```python
if x is None:
    ...
```

and:

```python
if x is not None:
    ...
```

Do not normally use equality for this purpose.

## 6.4 Functions and `None`

A function that does not explicitly return a value returns `None`.

```python
def test():
    print("hello")
```

Then:

```python
result = test()
```

`result` becomes:

```text
None
```

This is different from the function not executing.

---

# 7. Truthiness and Boolean Evaluation

## 7.1 Python does not require every condition to literally be `True` or `False`

Many objects have a truth value.

Example:

```python
if 10:
    print("yes")
```

This executes because `10` is truthy.

## 7.2 Common false values

The following are generally false in boolean contexts:

```text
False
None
0
0.0
0j
""
[]
()
{}
set()
```

Most other objects are truthy unless their type defines otherwise.

## 7.3 Practical meaning

Instead of:

```python
if len(items) != 0:
```

you can write:

```python
if items:
```

Instead of:

```python
if len(items) == 0:
```

you can write:

```python
if not items:
```

This is a very common Python style.

---

# 8. Strings — `str`

## 8.1 What is a string?

A string is an immutable sequence of Unicode characters.

```python
name = "Venkatesh"
```

Strings can use:

```python
"hello"
'hello'
```

Triple quotes are useful for multiline strings:

```python
text = """line one
line two
line three"""
```

## 8.2 Strings are sequences

Because strings are sequences, they support:

```text
indexing
slicing
iteration
membership testing
length
```

Example:

```python
s = "Python"
```

Indexes:

```text
 P  y  t  h  o  n
 0  1  2  3  4  5
```

Negative indexes:

```text
 P   y   t   h   o   n
-6  -5  -4  -3  -2  -1
```

Therefore:

```python
s[0]
```

is:

```text
P
```

and:

```python
s[-1]
```

is:

```text
n
```

## 8.3 String slicing

General form:

```python
sequence[start:stop:step]
```

The `stop` index is excluded.

```python
s = "Python"

s[0:3]
```

produces:

```text
Pyt
```

## 8.4 Negative slicing

```python
s[::-1]
```

creates a reversed string.

Because strings are immutable, this creates a new string rather than modifying the original.

## 8.5 String immutability

This is invalid:

```python
s = "hello"
s[0] = "H"
```

Instead:

```python
s = "H" + s[1:]
```

## 8.6 String concatenation

```python
first = "Hello"
second = "World"

result = first + " " + second
```

## 8.7 String repetition

```python
"abc" * 3
```

produces:

```text
abcabcabc
```

## 8.8 Membership

```python
"py" in "python"
```

returns:

```text
True
```

## 8.9 Important string methods

### Case conversion

```python
s.lower()
s.upper()
s.casefold()
s.capitalize()
s.title()
s.swapcase()
```

### Searching

```python
s.find(sub)
s.rfind(sub)
s.index(sub)
s.rindex(sub)
s.count(sub)
```

Important distinction:

```python
find()
```

returns `-1` when not found.

```python
index()
```

raises an exception when not found.

### Validation

```python
s.isalpha()
s.isdigit()
s.isalnum()
s.islower()
s.isupper()
s.isspace()
s.istitle()
s.isdecimal()
s.isnumeric()
```

### Removing whitespace

```python
s.strip()
s.lstrip()
s.rstrip()
```

These return new strings.

### Replacing

```python
s.replace(old, new)
```

Example:

```python
"hello world".replace("world", "Python")
```

### Splitting

```python
"a,b,c".split(",")
```

produces:

```python
["a", "b", "c"]
```

### Joining

```python
",".join(["a", "b", "c"])
```

produces:

```text
a,b,c
```

The object before `.join()` is the separator.

## 8.10 String formatting

Modern Python commonly uses f-strings:

```python
name = "Alex"
age = 20

print(f"My name is {name} and I am {age}")
```

Expressions can also be placed inside:

```python
print(f"{10 + 20}")
```

Formatting specifications:

```python
x = 3.14159

print(f"{x:.2f}")
```

produces two decimal places.

## 8.11 Escape sequences

Examples:

```text
\n  newline
\t  tab
\\  backslash
\"  double quote
\'  single quote
```

## 8.12 Raw strings

Raw strings are useful when backslashes should generally be treated literally.

```python
r"C:\Users\Name"
```

They are particularly useful for regular-expression patterns and Windows-style paths.

## 8.13 Unicode

Python strings are Unicode-based, allowing text from many writing systems.

```python
text = "Hello नमस्ते 世界"
```

Characters can be converted using:

```python
ord(character)
chr(number)
```

---

# 9. Lists

## 9.1 What is a list?

A list is a mutable ordered collection.

```python
numbers = [10, 20, 30]
```

Lists can contain values of different types:

```python
data = [10, "hello", 3.14, True]
```

Although Python allows this, keeping a logically consistent collection is usually easier to reason about.

## 9.2 Indexing

```python
numbers[0]
numbers[-1]
```

## 9.3 Slicing

```python
numbers[start:stop:step]
```

Slicing creates a new list.

## 9.4 Lists are mutable

```python
numbers = [10, 20, 30]
numbers[1] = 200
```

Now:

```python
[10, 200, 30]
```

## 9.5 `append()`

Adds one object at the end.

```python
a = [1, 2]
a.append(3)
```

Result:

```text
[1, 2, 3]
```

If you write:

```python
a.append([4, 5])
```

the list becomes:

```text
[1, 2, 3, [4, 5]]
```

## 9.6 `extend()`

Adds elements from another iterable.

```python
a = [1, 2]
a.extend([3, 4])
```

Result:

```text
[1, 2, 3, 4]
```

Important:

```text
append(x) → adds x as one element

extend(x) → adds elements from x
```

## 9.7 `insert()`

```python
a.insert(index, value)
```

Example:

```python
a.insert(1, 100)
```

## 9.8 Removing elements

```python
a.remove(value)
```

removes the first matching value.

If the value does not exist, it raises:

```text
ValueError
```

## 9.9 `pop()`

```python
a.pop()
```

removes and returns the last element.

```python
a.pop(index)
```

removes and returns an element at the specified index.

Invalid index:

```text
IndexError
```

## 9.10 Other important list methods

```python
a.clear()
a.index(value)
a.count(value)
a.reverse()
a.sort()
a.copy()
```

## 9.11 `sort()` versus `sorted()`

`list.sort()` modifies the existing list:

```python
a.sort()
```

It returns:

```text
None
```

`sorted()` creates and returns a new sorted list:

```python
b = sorted(a)
```

This distinction is extremely important.

## 9.12 Sorting options

```python
sorted(items)
sorted(items, reverse=True)
sorted(items, key=function)
```

Similarly:

```python
items.sort(reverse=True)
items.sort(key=function)
```

The `key` argument tells Python what value should be used for comparison.

## 9.13 Copying a list

```python
b = a
```

does not copy the list.

A shallow copy can be made using:

```python
b = a.copy()
```

or:

```python
b = a[:]
```

or:

```python
b = list(a)
```

Nested mutable objects require deeper consideration, discussed later.

---

# 10. Tuples

## 10.1 What is a tuple?

A tuple is an ordered immutable collection.

```python
t = (10, 20, 30)
```

It supports:

```text
indexing
slicing
iteration
membership
unpacking
```

but its structure cannot be modified after creation.

## 10.2 Tuple creation

```python
t = (1, 2, 3)
```

Parentheses are not the fundamental reason it is a tuple.

The comma is important.

A single-element tuple is:

```python
t = (10,)
```

Not:

```python
t = (10)
```

The latter is simply:

```text
10
```

## 10.3 Tuple packing

```python
t = 10, 20, 30
```

Python packs the values into a tuple.

## 10.4 Tuple unpacking

```python
a, b, c = (10, 20, 30)
```

Conceptually:

```text
a → 10
b → 20
c → 30
```

## 10.5 Tuple methods

Tuples have relatively few methods because they are immutable.

```python
t.count(value)
t.index(value)
```

## 10.6 Important subtlety

A tuple itself is immutable, but it can contain mutable objects.

Example:

```python
t = ([1, 2], [3, 4])
```

You cannot replace an element of the tuple:

```python
t[0] = [5, 6]
```

But the list inside it can still be modified:

```python
t[0].append(3)
```

So:

```text
tuple immutable
        +
mutable object inside tuple
        =
tuple's references cannot change, but contained mutable objects can change
```

---

# 11. Sets and `frozenset`

## 11.1 What is a set?

A set is a collection of unique elements.

```python
s = {1, 2, 3}
```

Duplicate values are eliminated:

```python
s = {1, 2, 2, 3, 3}
```

Conceptually:

```text
{1, 2, 3}
```

## 11.2 Sets are not indexed sequences

You cannot rely on positional access such as:

```python
s[0]
```

Sets are designed around membership and set operations rather than positional indexing.

## 11.3 Empty set

This is an important syntax exception:

```python
{}
```

creates an empty dictionary.

An empty set is:

```python
set()
```

## 11.4 Adding elements

```python
s.add(x)
```

Add multiple elements from an iterable:

```python
s.update(iterable)
```

## 11.5 Removing elements

```python
s.remove(x)
```

raises `KeyError` if the element does not exist.

```python
s.discard(x)
```

does nothing if the element does not exist.

This distinction is important.

## 11.6 Other methods

```python
s.pop()
s.clear()
```

`set.pop()` removes and returns an arbitrary element. Do not interpret it as "remove the last element."

## 11.7 Set operations

Union:

```python
a | b
```

or:

```python
a.union(b)
```

Intersection:

```python
a & b
```

Difference:

```python
a - b
```

Symmetric difference:

```python
a ^ b
```

## 11.8 Relationship tests

```python
a.issubset(b)
a.issuperset(b)
a.isdisjoint(b)
```

Operators are also available for several of these relationships:

```python
a <= b
a >= b
```

## 11.9 Hashability

Set elements must be hashable.

This is why:

```python
{1, 2, 3}
```

is valid.

But:

```python
{[1, 2]}
```

is invalid because lists are mutable and therefore unhashable.

## 11.10 `frozenset`

A `frozenset` is an immutable set.

```python
fs = frozenset([1, 2, 3])
```

It can be used in places where a hashable set-like object is needed.

---

# 12. Dictionaries

## 12.1 What is a dictionary?

A dictionary stores key-value associations.

```python
student = {
    "name": "Alex",
    "age": 20,
    "marks": 95
}
```

Conceptually:

```text
key       → value

"name"    → "Alex"
"age"     → 20
"marks"   → 95
```

## 12.2 Keys and values

Keys identify entries.

Keys must be hashable.

Common key types include:

```text
str
int
float
tuple containing hashable values
frozenset
```

Mutable types such as lists cannot normally be dictionary keys.

## 12.3 Keys must be unique

```python
d = {
    "a": 10,
    "a": 20
}
```

The later assignment replaces the earlier value.

The resulting mapping contains one `"a"` key with value `20`.

## 12.4 Accessing values

```python
d["name"]
```

If the key does not exist:

```text
KeyError
```

Alternative:

```python
d.get("name")
```

If the key is missing, `get()` returns `None` by default.

You can provide another default:

```python
d.get("name", "Unknown")
```

## 12.5 Adding and updating

```python
d["age"] = 21
```

If the key exists, its value is replaced.

If it does not exist, a new key-value pair is created.

## 12.6 `update()`

```python
d.update({
    "age": 21,
    "city": "Hyderabad"
})
```

It updates existing keys and adds new ones.

## 12.7 Removing entries

```python
del d["age"]
```

If the key is missing:

```text
KeyError
```

`pop()`:

```python
value = d.pop("age")
```

removes the key and returns its value.

`popitem()` removes and returns a key-value pair according to dictionary's defined insertion-order behavior.

## 12.8 `setdefault()`

```python
d.setdefault("count", 0)
```

If `"count"` does not exist, it inserts the default.

If it already exists, its existing value remains.

This is useful when you want:

```text
get existing value
OR
create default value if absent
```

## 12.9 Dictionary views

```python
d.keys()
d.values()
d.items()
```

These return view objects rather than ordinary lists.

For example:

```python
for key in d:
    print(key)
```

iterates over keys.

You can write:

```python
for key, value in d.items():
    print(key, value)
```

## 12.10 Dictionary insertion order

Modern Python dictionaries preserve insertion order.

Example:

```python
d = {}

d["a"] = 10
d["b"] = 20
d["c"] = 30
```

Iteration follows insertion order.

However, do not confuse:

```text
insertion order
```

with:

```text
sorted order
```

The dictionary does not automatically sort keys.

## 12.11 Dictionary comprehensions

```python
squares = {x: x * x for x in range(5)}
```

## 12.12 Nested dictionaries

Dictionaries can contain dictionaries:

```python
students = {
    "A": {
        "age": 20,
        "marks": 90
    },
    "B": {
        "age": 21,
        "marks": 95
    }
}
```

Access:

```python
students["A"]["marks"]
```

---

# 13. Operators

## 13.1 Arithmetic operators

```text
+   addition
-   subtraction
*   multiplication
/   division
//  floor division
%   modulo
**  exponentiation
```

## 13.2 Comparison operators

```text
==
!=
<
>
<=
>=
```

They produce boolean results.

## 13.3 Logical operators

```python
and
or
not
```

Python's `and` and `or` are particularly important because they do not necessarily return `True` or `False`.

For example:

```python
x = 0
y = 10

result = x or y
```

The result is:

```text
10
```

This is because `or` returns an operand based on truthiness.

Similarly:

```python
result = x and y
```

may return `x`.

Therefore:

> `and` and `or` are logical operators, but their result is an operand, not necessarily a boolean.

## 13.4 Assignment operators

```python
x = 10
```

Augmented assignment:

```python
x += 5
x -= 5
x *= 5
x /= 5
x //= 5
x %= 5
x **= 5
```

Bitwise augmented assignments also exist.

## 13.5 Bitwise operators

Python supports:

```text
&
|
^
~
<<
>>
```

These operate on integer bit representations.

They are language operators, but their algorithmic applications are outside the scope of these notes.

## 13.6 Membership operators

```python
in
not in
```

Example:

```python
3 in [1, 2, 3]
```

For dictionaries:

```python
"a" in d
```

checks keys, not values.

## 13.7 Identity operators

```python
is
is not
```

These compare object identity.

Do not use `is` as a general replacement for `==`.

## 13.8 Conditional expression

Python provides a compact conditional expression:

```python
result = value1 if condition else value2
```

Conceptually:

```text
if condition:
    result = value1
else:
    result = value2
```

---

# 14. Operator Precedence

Python evaluates expressions according to precedence rules.

A simplified important order is:

```text
parentheses
      ↓
exponentiation
      ↓
unary + - ~
      ↓
multiplication / // %
      ↓
addition / subtraction
      ↓
shifts
      ↓
bitwise &
      ↓
bitwise ^
      ↓
bitwise |
      ↓
comparisons / in / is
      ↓
not
      ↓
and
      ↓
or
      ↓
conditional expression
```

When an expression becomes difficult to read, use parentheses.

Prefer:

```python
(a + b) * c
```

over relying on memory of precedence.

---

# 15. Input and Output

## 15.1 `input()`

```python
name = input()
```

The most important fact:

> `input()` returns a string.

Even if the user enters:

```text
100
```

the result is:

```python
"100"
```

not:

```python
100
```

Therefore:

```python
age = int(input())
```

is commonly used for integer input.

For floating-point:

```python
value = float(input())
```

## 15.2 Prompt

```python
name = input("Enter your name: ")
```

## 15.3 `print()`

```python
print("Hello")
```

Multiple values:

```python
print("Age:", age)
```

## 15.4 `sep`

```python
print(1, 2, 3, sep=",")
```

## 15.5 `end`

Normally `print()` ends with a newline.

You can change it:

```python
print("Hello", end=" ")
print("World")
```

## 15.6 `print()` returns `None`

```python
x = print("hello")
```

The output is displayed, but:

```python
x
```

is:

```text
None
```

---

# 16. Conditional Statements

## 16.1 `if`

```python
if condition:
    statement
```

Example:

```python
if age >= 18:
    print("Adult")
```

## 16.2 `if / else`

```python
if condition:
    ...
else:
    ...
```

## 16.3 `if / elif / else`

```python
if condition1:
    ...
elif condition2:
    ...
else:
    ...
```

Conditions are checked from top to bottom.

Once one condition is true, its block executes and the remaining branches are skipped.

## 16.4 Nested conditions

```python
if condition1:
    if condition2:
        ...
```

Indentation determines nesting.

---

# 17. Loops

## 17.1 `while`

A `while` loop repeatedly executes while its condition is truthy.

```python
while condition:
    statement
```

Mental model:

```text
check condition
      ↓
true?
 ├── yes → execute body → check again
 └── no  → stop
```

## 17.2 `for`

Python's `for` loop iterates over an iterable.

```python
for item in iterable:
    ...
```

This is an important conceptual difference from thinking of `for` merely as a numeric counter loop.

Examples:

```python
for x in [10, 20, 30]:
    print(x)
```

```python
for ch in "Python":
    print(ch)
```

## 17.3 `range()`

`range()` produces a range object.

Forms:

```python
range(stop)
range(start, stop)
range(start, stop, step)
```

Example:

```python
for i in range(5):
    print(i)
```

produces:

```text
0
1
2
3
4
```

The stop value is excluded.

## 17.4 `break`

Immediately exits the nearest loop.

```python
for x in items:
    if condition:
        break
```

## 17.5 `continue`

Skips the remaining body of the current iteration.

```python
for x in items:
    if condition:
        continue
    print(x)
```

## 17.6 `pass`

`pass` does nothing.

It is useful when syntax requires a statement but you intentionally have no implementation yet.

```python
if condition:
    pass
```

## 17.7 Loop `else`

Python allows:

```python
for item in items:
    ...
else:
    ...
```

The `else` block executes when the loop finishes normally, rather than being terminated by `break`.

The same concept applies to `while`.

This is a Python-specific control-flow feature that is worth understanding before assuming `else` always means "otherwise."

---

# 18. `enumerate()`, `zip()`, and Unpacking

## 18.1 `enumerate()`

When you need both an index and a value:

```python
for index, value in enumerate(items):
    print(index, value)
```

Conceptually:

```text
item
 ↓
(index, item)
```

The optional starting index:

```python
enumerate(items, start=1)
```

## 18.2 `zip()`

Combines corresponding elements from iterables.

```python
names = ["A", "B", "C"]
marks = [90, 80, 95]

for name, mark in zip(names, marks):
    print(name, mark)
```

By default, `zip()` stops when the shortest iterable is exhausted.

Modern Python also supports:

```python
zip(a, b, strict=True)
```

when you want mismatched lengths to raise an error.

## 18.3 Unpacking

```python
a, b = [10, 20]
```

Starred unpacking:

```python
first, *middle, last = [1, 2, 3, 4, 5]
```

Results conceptually:

```text
first  → 1
middle → [2, 3, 4]
last   → 5
```

---

# 19. Functions

## 19.1 What is a function?

A function is a reusable unit of behavior.

It allows you to:

```text
define behavior once
give it a name
provide inputs
perform operations
return a result
```

General form:

```python
def function_name(parameters):
    statements
    return result
```

## 19.2 Defining a function

```python
def add(a, b):
    return a + b
```

Calling:

```python
result = add(10, 20)
```

## 19.3 Parameters and arguments

In:

```python
def add(a, b):
    ...
```

`a` and `b` are parameters.

In:

```python
add(10, 20)
```

`10` and `20` are arguments.

## 19.4 Return

```python
return value
```

returns a value to the caller.

Example:

```python
def square(x):
    return x * x
```

## 19.5 Function without `return`

```python
def hello():
    print("Hello")
```

Calling:

```python
result = hello()
```

causes:

```text
Hello
```

to be printed.

But:

```python
result == None
```

## 19.6 Multiple return values

Python allows:

```python
def get_values():
    return 10, 20
```

This actually returns a tuple:

```text
(10, 20)
```

You can unpack it:

```python
a, b = get_values()
```

## 19.7 Positional arguments

```python
def greet(name, age):
    ...
```

Call:

```python
greet("Alex", 20)
```

Arguments are matched by position.

## 19.8 Keyword arguments

```python
greet(age=20, name="Alex")
```

The order can differ because names identify the parameters.

## 19.9 Default parameters

```python
def greet(name="Guest"):
    print(name)
```

Then:

```python
greet()
```

uses:

```text
Guest
```

while:

```python
greet("Alex")
```

uses:

```text
Alex
```

## 19.10 The mutable default argument trap

This is a classic Python issue.

Avoid:

```python
def add_item(item, items=[]):
    items.append(item)
    return items
```

The default list is created once when the function definition is evaluated, not freshly created for every call.

Prefer:

```python
def add_item(item, items=None):
    if items is None:
        items = []

    items.append(item)
    return items
```

This is one of the most important Python-specific pitfalls.

## 19.11 `*args`

Allows a function to receive a variable number of positional arguments.

```python
def total(*args):
    ...
```

Inside the function:

```text
args → tuple containing positional arguments
```

Example:

```python
total(1, 2, 3, 4)
```

## 19.12 `**kwargs`

Allows a function to receive variable keyword arguments.

```python
def show(**kwargs):
    ...
```

Inside:

```text
kwargs → dictionary
```

## 19.13 Positional-only parameters

Python supports parameters that must be supplied positionally.

```python
def function(a, b, /):
    ...
```

`a` and `b` cannot be passed by keyword.

## 19.14 Keyword-only parameters

Parameters after `*` can be made keyword-only:

```python
def function(a, *, option=False):
    ...
```

Then:

```python
function(10, option=True)
```

is valid.

But:

```python
function(10, True)
```

is not.

## 19.15 Argument unpacking

Given:

```python
values = [10, 20]
```

You can call:

```python
add(*values)
```

Dictionary unpacking:

```python
data = {
    "name": "Alex",
    "age": 20
}
```

Can be used with:

```python
function(**data)
```

when parameter names match.

---

# 20. Scope and Namespaces

## 20.1 What is scope?

Scope determines where a name can be accessed.

Python commonly follows the LEGB lookup model:

```text
L → Local
E → Enclosing
G → Global
B → Built-in
```

## 20.2 Local scope

```python
def test():
    x = 10
```

`x` is local to that function.

## 20.3 Global scope

```python
x = 10

def test():
    print(x)
```

The function can read the global name.

## 20.4 Local assignment

If you assign to a name inside a function, Python generally treats it as local to that function unless explicitly declared otherwise.

```python
x = 10

def test():
    x = 20
```

This creates/rebinds a local `x`; it does not modify the global `x`.

## 20.5 `global`

```python
x = 10

def change():
    global x
    x = 20
```

This tells Python that assignments to `x` refer to the global name.

Use this carefully because excessive global state makes programs harder to reason about.

## 20.6 `nonlocal`

Used in nested functions to modify a variable in an enclosing function scope.

```python
def outer():
    x = 10

    def inner():
        nonlocal x
        x += 1

    inner()
```

`nonlocal` does not refer to the module/global scope.

---

# 21. Functions Are First-Class Objects

Python functions themselves are objects.

Therefore a function can be:

```text
stored in a variable
passed to another function
returned from a function
stored in a collection
```

Example:

```python
def square(x):
    return x * x

f = square
```

Now:

```python
f(5)
```

works.

The name `f` refers to the same function object.

## 21.1 Passing functions

```python
def apply(function, value):
    return function(value)
```

Then:

```python
apply(square, 5)
```

This concept is the foundation for tools such as:

```python
sorted(..., key=...)
map(...)
filter(...)
```

---

# 22. Lambda Functions

## 22.1 What is a lambda?

A lambda is a small anonymous function expression.

```python
lambda x: x * 2
```

Equivalent conceptually to:

```python
def double(x):
    return x * 2
```

## 22.2 Example

```python
double = lambda x: x * 2
```

Then:

```python
double(5)
```

returns:

```text
10
```

Lambdas are best used for short expressions.

Do not force complicated logic into a lambda merely to make code shorter.

---

# 23. Comprehensions

Comprehensions are Python syntax for constructing collections from iterables.

## 23.1 List comprehension

```python
squares = [x * x for x in range(5)]
```

Conceptually:

```text
for each x
    calculate x*x
    put result into list
```

## 23.2 Conditional comprehension

```python
values = [x for x in range(10) if x % 2 == 0]
```

The structure is:

```python
[expression for item in iterable if condition]
```

## 23.3 Set comprehension

```python
s = {x * x for x in range(5)}
```

## 23.4 Dictionary comprehension

```python
d = {x: x * x for x in range(5)}
```

## 23.5 Generator expression

```python
g = (x * x for x in range(5))
```

Unlike a list comprehension, it does not immediately construct the entire list.

It produces values lazily as requested.

## 23.6 Nested comprehensions

Python permits:

```python
result = [
    x
    for row in matrix
    for x in row
]
```

However, comprehensions should remain readable. If the expression becomes difficult to understand, use ordinary loops.

---

# 24. Iterables and Iterators

## 24.1 What is an iterable?

An iterable is an object that can provide its elements one at a time for iteration.

Examples:

```text
list
tuple
string
set
dictionary
range
file
```

You can commonly use them in:

```python
for item in iterable:
    ...
```

## 24.2 What is an iterator?

An iterator is an object that produces the next value when requested.

Conceptually:

```text
iterator
   ↓
next value
   ↓
next value
   ↓
next value
```

Python provides:

```python
iter()
next()
```

## 24.3 Example

```python
numbers = [10, 20, 30]

it = iter(numbers)

print(next(it))
print(next(it))
print(next(it))
```

Output:

```text
10
20
30
```

After all values are consumed:

```python
next(it)
```

raises:

```text
StopIteration
```

## 24.4 `for` loop mental model

A useful conceptual model is:

```text
obtain iterator
      ↓
request next value
      ↓
execute loop body
      ↓
request next value
      ↓
repeat
      ↓
StopIteration
      ↓
finish loop
```

You normally do not need to manually write this mechanism, but understanding it explains how Python's `for` loop works.

---

# 25. Generators

## 25.1 What is a generator?

A generator is a convenient way to produce values lazily.

A generator function uses:

```python
yield
```

Example:

```python
def numbers():
    yield 1
    yield 2
    yield 3
```

Calling:

```python
g = numbers()
```

does not immediately execute the whole function.

Values are produced when requested.

```python
next(g)
```

returns:

```text
1
```

Next:

```python
next(g)
```

returns:

```text
2
```

## 25.2 `yield` versus `return`

`return` finishes the function and returns a result.

`yield` temporarily suspends the generator and produces a value.

Conceptually:

```text
yield
 ↓
pause function
 ↓
give value to caller
 ↓
resume later
```

## 25.3 Why generators matter

Generators are useful when values can be processed one at a time instead of creating a complete collection immediately.

This is a language/runtime feature rather than a DSA technique.

---

# 26. Built-in Functions

Python provides many built-in functions.

## 26.1 Basic inspection

```python
type(x)
isinstance(x, T)
id(x)
len(x)
```

## 26.2 Numeric

```python
abs(x)
round(x)
pow(x, y)
divmod(a, b)
sum(iterable)
min(iterable)
max(iterable)
```

## 26.3 Conversion

```python
int(x)
float(x)
complex(x)
bool(x)
str(x)
list(x)
tuple(x)
set(x)
dict(x)
frozenset(x)
bytes(x)
bytearray(x)
```

## 26.4 Character conversion

```python
ord("A")
chr(65)
```

## 26.5 Binary representation

```python
bin(10)
hex(255)
oct(10)
```

## 26.6 Iteration helpers

```python
iter(x)
next(iterator)
enumerate(iterable)
zip(a, b)
reversed(sequence)
sorted(iterable)
```

## 26.7 Logical helpers

```python
all(iterable)
any(iterable)
```

`all()` is true when all elements are truthy.

`any()` is true when at least one element is truthy.

## 26.8 `range()`

```python
range(10)
range(2, 10)
range(2, 10, 2)
```

It represents an arithmetic progression of integer values.

## 26.9 `map()`

```python
map(function, iterable)
```

It applies a function to elements and produces an iterator-like result.

Example:

```python
result = map(int, ["10", "20", "30"])
```

To materialize:

```python
list(result)
```

## 26.10 `filter()`

```python
filter(function, iterable)
```

Keeps elements for which the function evaluates as truthy.

It also produces an iterator-like result.

## 26.11 `reversed()`

Returns an iterator that traverses a reversible object in reverse order.

```python
for x in reversed(items):
    ...
```

## 26.12 `repr()` and `str()`

```python
str(x)
repr(x)
```

`str()` is intended as a readable representation.

`repr()` aims to provide a more explicit representation useful for debugging and development.

## 26.13 `hash()`

```python
hash(x)
```

Produces a hash value for hashable objects.

Hashability is important for:

```text
dictionary keys
set elements
```

## 26.14 `dir()`

```python
dir(object)
```

helps inspect available attributes and methods.

It is primarily an exploration/debugging tool.

## 26.15 `help()`

```python
help(object)
```

provides documentation interactively.

## 26.16 `callable()`

```python
callable(x)
```

checks whether an object can be called.

Functions are callable.

---

# 27. Exceptions and Error Handling

## 27.1 What is an exception?

An exception represents an abnormal condition detected during program execution.

Examples:

```text
invalid index
missing dictionary key
invalid value
wrong operation between types
division by zero
missing file
```

## 27.2 Common exceptions

### `SyntaxError`

Python cannot understand the source code syntax.

### `IndentationError`

Indentation violates Python's syntax rules.

### `NameError`

A name is not defined.

```python
print(x)
```

when `x` has never been defined.

### `TypeError`

An operation is inappropriate for the object's type.

```python
10 + "20"
```

### `ValueError`

The type may be appropriate, but the particular value is invalid.

```python
int("hello")
```

### `IndexError`

Sequence index is out of range.

```python
a = [1, 2]
a[10]
```

### `KeyError`

Dictionary/set operation refers to a missing key/element where that operation requires its existence.

### `AttributeError`

An object does not provide the requested attribute or method.

### `ZeroDivisionError`

Division by zero.

### `FileNotFoundError`

Requested file does not exist.

### `ModuleNotFoundError`

Python cannot locate the requested module.

### `ImportError`

An import operation fails for another import-related reason.

### `UnboundLocalError`

A local variable is referenced before it has been assigned in the relevant local scope.

### `RecursionError`

Execution exceeds Python's recursion limit.

## 27.3 `try`

Potentially failing code can be placed inside:

```python
try:
    risky_operation()
```

## 27.4 `except`

```python
try:
    risky_operation()
except ValueError:
    handle_error()
```

## 27.5 Multiple exceptions

```python
try:
    ...
except ValueError:
    ...
except TypeError:
    ...
```

## 27.6 `as`

You can access the exception object:

```python
try:
    ...
except ValueError as e:
    print(e)
```

## 27.7 `else`

The `else` block executes if no exception occurred in the `try` block.

```python
try:
    ...
except ValueError:
    ...
else:
    ...
```

## 27.8 `finally`

The `finally` block is used for cleanup code that should normally execute whether an exception occurred or not.

```python
try:
    ...
except:
    ...
finally:
    cleanup()
```

## 27.9 `raise`

You can explicitly raise an exception:

```python
raise ValueError("Invalid value")
```

## 27.10 Avoid bare `except`

This:

```python
except:
    ...
```

can catch far more than you intended.

Prefer specific exceptions:

```python
except ValueError:
    ...
```

or, when appropriate:

```python
except Exception:
    ...
```

---

# 28. Assertions

Python provides:

```python
assert condition
```

or:

```python
assert condition, "message"
```

Example:

```python
x = 10
assert x > 0
```

If the condition is false, Python raises:

```text
AssertionError
```

Assertions are useful for expressing assumptions during development.

They should not be treated as a replacement for normal user-input validation.

---

# 29. File Handling

## 29.1 Opening a file

```python
file = open("data.txt", "r")
```

Common modes:

```text
r  → read
w  → write
a  → append
x  → create exclusively
b  → binary mode
t  → text mode
+  → read and write
```

Examples:

```python
open("file.txt", "r")
open("file.txt", "w")
open("file.txt", "rb")
```

## 29.2 Reading

```python
data = file.read()
```

Read one line:

```python
line = file.readline()
```

Read all lines:

```python
lines = file.readlines()
```

## 29.3 Writing

```python
file.write("Hello")
```

Multiple strings:

```python
file.writelines(lines)
```

`writelines()` does not automatically insert newline characters between strings.

## 29.4 Closing files

A manually opened file should be closed:

```python
file.close()
```

## 29.5 `with`

Preferred:

```python
with open("data.txt", "r") as file:
    data = file.read()
```

The `with` statement handles resource cleanup when leaving the block.

This is an important Python language feature.

## 29.6 Encoding

Text files involve character encoding.

A common explicit form is:

```python
with open("data.txt", "r", encoding="utf-8") as file:
    data = file.read()
```

Being explicit about encoding is often safer when working across systems.

---

# 30. Modules and Imports

## 30.1 What is a module?

A module is a Python file containing Python code.

For example:

```text
math_tools.py
```

can contain functions and variables.

Another file can import it.

## 30.2 Importing

```python
import math
```

Then:

```python
math.sqrt(25)
```

## 30.3 Import specific names

```python
from math import sqrt
```

Then:

```python
sqrt(25)
```

## 30.4 Aliases

```python
import math as m
```

Then:

```python
m.sqrt(25)
```

## 30.5 Why imports exist

Modules allow code to be organized into separate files rather than placing everything into one huge source file.

They provide:

```text
organization
reuse
namespaces
separation of responsibilities
```

## 30.6 `__name__`

Python modules have a special variable:

```python
__name__
```

When a file is executed directly, it commonly has:

```python
__name__ == "__main__"
```

Therefore:

```python
if __name__ == "__main__":
    main()
```

is commonly used to distinguish:

```text
direct execution
```

from:

```text
being imported as a module
```

---

# 31. Namespaces

A namespace is a mapping from names to objects.

Examples include:

```text
local namespace
global/module namespace
built-in namespace
```

You can inspect a namespace using functions such as:

```python
globals()
locals()
```

You generally do not need to manipulate these directly during normal programming, but understanding the concept explains how Python resolves names.

---

# 32. Copying and Aliasing

## 32.1 Assignment is not copying

```python
a = [1, 2, 3]
b = a
```

There is one list.

```text
a ──┐
    ├──→ [1, 2, 3]
b ──┘
```

## 32.2 Shallow copy

```python
b = a.copy()
```

Now:

```text
a → list A
b → list B
```

The outer lists are different.

## 32.3 Nested objects

Consider:

```python
a = [[1, 2], [3, 4]]
b = a.copy()
```

The outer list is copied, but the inner lists are still shared.

Conceptually:

```text
a → outer A ──→ inner 1
             └→ inner 2

b → outer B ──→ inner 1
             └→ inner 2
```

Therefore modifying:

```python
b[0].append(100)
```

also affects:

```python
a[0]
```

## 32.4 Deep copy

The `copy` module provides:

```python
import copy

b = copy.deepcopy(a)
```

This recursively copies nested objects where appropriate.

Use deep copying deliberately; it is not always necessary or desirable.

---

# 33. A Major Python Pitfall — Repeating Mutable Objects

Consider:

```python
a = [[]] * 3
```

A beginner may expect:

```text
[[], [], []]
```

with three independent lists.

But the three positions refer to the same inner list.

Conceptually:

```text
a[0] ──┐
a[1] ──┼──→ same list
a[2] ──┘
```

Therefore:

```python
a[0].append(10)
```

can result in:

```python
[[10], [10], [10]]
```

The safer pattern for independent nested lists is:

```python
a = [[] for _ in range(3)]
```

This creates a new list for each iteration.

---

# 34. Bytes and Bytearray

## 34.1 `bytes`

`bytes` represents immutable binary data.

Example:

```python
data = b"hello"
```

It is different from:

```python
"hello"
```

which is a Unicode string.

## 34.2 Encoding a string

```python
text = "hello"
data = text.encode("utf-8")
```

Conceptually:

```text
Unicode text
     ↓ encode
binary bytes
```

## 34.3 Decoding

```python
data.decode("utf-8")
```

Conceptually:

```text
bytes
  ↓ decode
string
```

## 34.4 `bytearray`

`bytearray` is mutable binary data.

```python
data = bytearray(b"hello")
```

Unlike `bytes`, its contents can be modified.

---

# 35. Type Annotations

Python allows optional type annotations.

```python
age: int = 20
name: str = "Alex"
```

Functions:

```python
def add(a: int, b: int) -> int:
    return a + b
```

## 35.1 Annotations do not normally enforce types

The annotation:

```python
a: int
```

does not automatically make Python reject every non-integer value.

Python remains dynamically typed.

Annotations primarily provide:

```text
documentation
editor support
static analysis
developer communication
```

## 35.2 Collection annotations

Modern Python syntax can express:

```python
numbers: list[int]
names: list[str]
scores: dict[str, int]
values: tuple[int, int]
```

Type hints are a tool for describing intended types, not a replacement for understanding Python's runtime type system.

---

# 36. Context Managers and `with`

The `with` statement provides a structured way to use resources that require setup and cleanup.

For example:

```python
with open("data.txt") as file:
    data = file.read()
```

Conceptually:

```text
enter resource
      ↓
execute block
      ↓
perform cleanup
```

This is why `with` is preferred for file handling.

The concept is broader than files; Python provides many context-manager-enabled resources.

---

# 37. Pattern Matching

Modern Python provides `match` and `case`.

Basic structure:

```python
match value:
    case pattern1:
        ...
    case pattern2:
        ...
    case _:
        ...
```

The `_` pattern acts as a catch-all pattern in this context.

Pattern matching is more expressive than a simple equality-based chain in many situations.

It is a modern Python feature and is not required for basic Python fluency, but it is part of the language.

---

# 38. Important Python-Specific Behavior

## 38.1 `input()` always returns text

```python
x = input()
```

Even if the user enters:

```text
100
```

`x` is:

```python
"100"
```

Convert explicitly:

```python
x = int(input())
```

## 38.2 `print()` returns `None`

```python
x = print("hello")
```

`x` becomes:

```text
None
```

## 38.3 Functions without return return `None`

```python
def f():
    pass
```

Then:

```python
f() is None
```

## 38.4 List methods that modify the list generally return `None`

For example:

```python
a = [3, 1, 2]
result = a.sort()
```

`a` is sorted, but:

```python
result
```

is:

```text
None
```

Do not write:

```python
a = a.sort()
```

because you will replace `a` with `None`.

## 38.5 Strings do not change in place

```python
s = "hello"
s.upper()
```

does not change `s`.

You need:

```python
s = s.upper()
```

because strings are immutable.

## 38.6 `remove()` and `pop()` are different

For lists:

```python
remove(value)
```

removes by value.

```python
pop(index)
```

removes by position and returns the removed value.

For sets:

```python
remove(value)
```

raises `KeyError` when missing.

```python
discard(value)
```

does not.

## 38.7 Dictionary membership checks keys

```python
d = {"a": 10}
```

Then:

```python
"a" in d
```

checks keys.

It does not search through values.

## 38.8 `range()` does not create a normal list

```python
r = range(1000000000)
```

does not mean that a billion integer objects are immediately stored in a normal list.

`range` is a specialized sequence-like object representing the progression.

## 38.9 `map()`, `filter()`, and `zip()` are lazy-style iterators

They generally do not immediately create ordinary lists.

Therefore:

```python
x = map(...)
```

and:

```python
list(x)
```

are conceptually different.

## 38.10 Slicing creates a new sequence

For common built-in sequences:

```python
b = a[:]
```

creates a new outer sequence.

It is not the same as:

```python
b = a
```

---

# 39. Common Errors and Their Real Causes

## 39.1 `NameError`

```python
print(age)
```

when `age` has never been defined.

Cause:

```text
Python cannot find the name in the relevant namespaces.
```

## 39.2 `TypeError`

```python
"10" + 20
```

Cause:

```text
operation is not supported between those object types.
```

## 39.3 `ValueError`

```python
int("abc")
```

Cause:

```text
the conversion operation is meaningful,
but this particular value cannot be converted.
```

## 39.4 `IndexError`

```python
a = [1, 2]
print(a[5])
```

Cause:

```text
index is outside the valid sequence range.
```

## 39.5 `KeyError`

```python
d = {"a": 10}
print(d["b"])
```

Cause:

```text
requested dictionary key does not exist.
```

## 39.6 `AttributeError`

```python
x = 10
x.append(5)
```

Cause:

```text
the integer object does not provide an append attribute/method.
```

## 39.7 `IndentationError`

Cause:

```text
block indentation does not satisfy Python syntax.
```

## 39.8 `SyntaxError`

Cause:

```text
Python cannot parse the source according to its grammar.
```

---

# 40. Common Python Mistakes and Their Solutions

## 40.1 Confusing `=` and `==`

```python
x = 10
```

means assignment.

```python
x == 10
```

means equality comparison.

## 40.2 Using `is` for ordinary value comparison

Incorrect idea:

```python
a is 10
```

Use:

```python
a == 10
```

For singleton objects such as `None`, use:

```python
a is None
```

## 40.3 Assuming assignment copies a list

```python
b = a
```

does not create an independent list.

Use:

```python
b = a.copy()
```

when a shallow copy is what you need.

## 40.4 Forgetting that strings are immutable

Incorrect:

```python
s[0] = "X"
```

Instead construct a new string.

## 40.5 Confusing `append()` and `extend()`

```python
a.append([3, 4])
```

adds one list element.

```python
a.extend([3, 4])
```

adds two elements.

## 40.6 Assigning the result of `sort()`

Wrong:

```python
a = a.sort()
```

Correct:

```python
a.sort()
```

or:

```python
a = sorted(a)
```

## 40.7 Forgetting `input()` returns `str`

Wrong when integer arithmetic is expected:

```python
a = input()
b = input()

print(a + b)
```

If inputs are:

```text
10
20
```

the output is:

```text
1020
```

because strings are concatenated.

Correct:

```python
a = int(input())
b = int(input())
```

## 40.8 Mutable default arguments

Avoid:

```python
def f(x=[]):
    ...
```

when the list is intended to be fresh for every call.

Use:

```python
def f(x=None):
    if x is None:
        x = []
```

## 40.9 Assuming dictionary keys are sorted

Insertion order is preserved, but automatic sorting does not happen.

## 40.10 Assuming set order

Sets should be treated as unordered collections for normal programming purposes.

Do not write logic that depends on an assumed positional order.

---

# 41. Python Collection Method Reference

## 41.1 List

```text
append(x)       → add one element
extend(iterable)→ add multiple elements
insert(i, x)    → insert at index
remove(x)       → remove first matching value
pop([i])        → remove and return element
clear()         → remove all elements
index(x)        → find first index
count(x)        → count occurrences
sort()          → sort in place
reverse()       → reverse in place
copy()          → shallow copy
```

## 41.2 Tuple

```text
count(x)
index(x)
```

## 41.3 Set

```text
add(x)
update(iterable)
remove(x)
discard(x)
pop()
clear()
union(...)
intersection(...)
difference(...)
symmetric_difference(...)
issubset(...)
issuperset(...)
isdisjoint(...)
```

## 41.4 Dictionary

```text
get(key)
keys()
values()
items()
update(...)
pop(key)
popitem()
setdefault(key)
clear()
copy()
```

---

# 42. Sequence Operations

Strings, lists, and tuples are examples of sequences.

Common operations include:

```python
len(sequence)
sequence[index]
sequence[start:stop]
sequence[start:stop:step]
value in sequence
value not in sequence
```

Iteration:

```python
for item in sequence:
    ...
```

Concatenation:

```python
a + b
```

Repetition:

```python
a * n
```

Not every sequence-like object supports every operation in exactly the same way, so always understand the specific type.

---

# 43. Built-in Data Structure Comparison

| Type        | Ordered             | Mutable | Duplicate Values | Indexing  |
| ----------- | ------------------- | ------- | ---------------- | --------- |
| `list`      | Yes                 | Yes     | Yes              | Yes       |
| `tuple`     | Yes                 | No      | Yes              | Yes       |
| `set`       | No positional order | Yes     | No               | No        |
| `frozenset` | No positional order | No      | No               | No        |
| `dict`      | Insertion order     | Yes     | Keys: No         | Key-based |
| `str`       | Yes                 | No      | Yes              | Yes       |

The most important conceptual distinction is:

```text
list     → mutable ordered collection
tuple    → immutable ordered collection
set      → unique-element collection
dict     → key-value mapping
str      → immutable text sequence
```

---

# 44. Python's Most Important Mental Models

## 44.1 Names point to objects

Think:

```text
name → object
```

rather than:

```text
variable = permanent box with fixed type
```

## 44.2 Objects have types

```python
x = 10
```

means:

```text
x → object of type int
```

Later:

```python
x = "hello"
```

means:

```text
x → object of type str
```

## 44.3 Mutable objects can change

```text
list
dict
set
bytearray
```

can have their contents modified.

## 44.4 Immutable objects cannot be modified in place

```text
int
float
bool
str
tuple
bytes
```

When you appear to "change" one, Python generally creates/rebinds to another object.

## 44.5 Assignment binds names

```python
b = a
```

means:

```text
b refers to the object currently referenced by a
```

It does not inherently mean:

```text
make an independent copy
```

## 44.6 Functions receive object references

A useful mental model is:

```text
caller name
    ↓
object
    ↑
parameter name inside function
```

This explains why mutating a mutable argument can be visible to the caller while rebinding the parameter does not rebind the caller's name.

---

# 45. Python Style and Readability

Python strongly emphasizes readable code.

Use:

```python
student_name
total_marks
calculate_average()
```

rather than unclear names such as:

```python
sn
tm
ca()
```

unless the short name is genuinely obvious from context.

Use four spaces for indentation.

Keep functions focused.

Prefer readable code over clever compressed syntax.

Use comments when they explain something that cannot be understood easily from the code itself.

Use docstrings to document functions when appropriate:

```python
def add(a, b):
    """Return the sum of two values."""
    return a + b
```

---

# 46. Important Differences in Python's Programming Model

## 46.1 No mandatory variable declaration

Names can be introduced simply by assignment:

```python
x = 10
```

## 46.2 Runtime type information is always associated with objects

Python determines operations based on the runtime objects involved.

## 46.3 Indentation defines blocks

Whitespace is not merely visual formatting in Python syntax.

## 46.4 Many operations are explicit

Python does not automatically convert arbitrary incompatible values merely because a conversion could theoretically be performed.

## 46.5 Memory management is automatic

Python manages object lifetime automatically.

You normally do not manually allocate and release ordinary objects.

## 46.6 Integer overflow behaves differently

Python's built-in integers can grow to very large values subject to available memory.

This differs from environments where ordinary integer types have a fixed maximum width.

## 46.7 Division behavior is distinct

```python
/
```

produces true division.

```python
//
```

performs floor division.

This distinction is essential.

## 46.8 Functions are objects

Functions can be passed around just like other Python objects.

## 46.9 Collections are highly integrated into the language

Lists, dictionaries, sets, tuples, unpacking, comprehensions, iteration, and generators are not merely external libraries; they are central parts of Python programming style.

---

# 47. A Complete Python Execution Mental Model

When Python executes:

```python
x = [10, 20]

y = x

y.append(30)
```

think through it step by step.

### Step 1

Create a list object:

```text
[10, 20]
```

### Step 2

Bind:

```text
x → list
```

### Step 3

Execute:

```python
y = x
```

Now:

```text
x ──┐
    ├──→ [10, 20]
y ──┘
```

### Step 4

Execute:

```python
y.append(30)
```

The list itself is mutated.

Now:

```text
x ──┐
    ├──→ [10, 20, 30]
y ──┘
```

Therefore:

```python
print(x)
```

produces:

```text
[10, 20, 30]
```

This mental model explains a huge portion of Python behavior.

---

# 48. Final Python Pre-OOP Checklist

Before moving to OOP, you should be comfortable with all of the following:

## Language Fundamentals

```text
Python execution model
statements
expressions
indentation
comments
identifiers
keywords
variables/names
assignment
identity
mutability
immutability
```

## Data Types

```text
int
float
complex
bool
None
str
list
tuple
set
frozenset
dict
bytes
bytearray
```

## Operators

```text
arithmetic
comparison
assignment
augmented assignment
logical
bitwise
membership
identity
conditional expression
```

## Strings

```text
indexing
slicing
immutability
Unicode
escape sequences
raw strings
formatting
f-strings
searching
validation
split
join
replace
strip
case conversion
```

## Collections

```text
list operations
tuple operations
set operations
dictionary operations
nested collections
copying
aliasing
hashability
```

## Control Flow

```text
if
elif
else
while
for
range
break
continue
pass
loop else
match/case
```

## Functions

```text
def
parameters
arguments
return
default arguments
positional arguments
keyword arguments
positional-only arguments
keyword-only arguments
*args
**kwargs
unpacking
scope
LEGB
global
nonlocal
lambda
first-class functions
```

## Iteration

```text
iterable
iterator
iter()
next()
StopIteration
enumerate()
zip()
map()
filter()
reversed()
generators
yield
generator expressions
```

## Python Tools

```text
len()
sum()
min()
max()
sorted()
all()
any()
abs()
round()
divmod()
type()
isinstance()
id()
hash()
dir()
help()
```

## Error Handling

```text
SyntaxError
IndentationError
NameError
TypeError
ValueError
IndexError
KeyError
AttributeError
ZeroDivisionError
FileNotFoundError
ModuleNotFoundError
ImportError
UnboundLocalError
RecursionError
try
except
else
finally
raise
assert
```

## Files and Modules

```text
open()
read()
write()
close()
with
encoding
import
from ... import ...
as
modules
packages
__name__
__main__
```

## Python-Specific Pitfalls

```text
== vs is
assignment vs copying
mutable vs immutable
append vs extend
remove vs pop
remove vs discard
sort() vs sorted()
input() returns str
print() returns None
functions without return return None
mutable default arguments
nested mutable aliasing
list repetition aliasing
dictionary membership checks keys
set order assumptions
float precision
floor division
truthiness
iterator exhaustion
```

# 49. The Core Rule to Remember

If you remember only one mental model from these notes, remember this:

```text
Python program
      ↓
names refer to objects
      ↓
objects have types
      ↓
objects may be mutable or immutable
      ↓
operations depend on object types
      ↓
functions receive references to objects
      ↓
collections store references to objects
      ↓
assignment binds names; it does not automatically copy objects
```

Once this model becomes natural, Python stops feeling like a collection of unrelated syntax rules.

The syntax becomes the surface.

The **object model, mutability, references, iteration, functions, scope, and dynamic typing** become the underlying theory that explains why the syntax behaves the way it does.
