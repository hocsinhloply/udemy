python -m venv venv ### Create venv in folder venv

venv\Scripts\activate.bat

jupyter notebook

`1+1 #Shift + Enter`

# Data Types
- Integers: int
- Floating point: float
- Strings: str
- Lists: list - Ordered sequence of objects
- Dictionaries: dict - Unordered Key: Value pairs
- Tuples: tup - Ordered immutable sequence of object
- Sets: set - Unordered collection of unique objects
- Booleans: bool

Modulo or "Mod" Operator: `7 / 4` `7 % 4`

# Variable
- Lowercase
- Avoid built-in keywords
- Using type() to determine type of variable

# String
- Sequences of characters
- Index: 0 1 2 3 4
- Reverse Index: 0 -4 -3 -2 -1
- Slicing: [start:stop:step]
- **start**: index for the silce start
- **stop**: index will go up to
- **step**: size "jump"

## Properties and Methods
- Immutability `name = "Sam", name[0] = 'P' => not support => create new string`

## Formatting with .format() method
## Float formatting follow {value:width.precision f}


# Lists
- Ordered sequence of objects
- Use [] brackets
- Support indexing and slicing

```
list_name.append(value) #  add new at tail
list_name.pop() # pop tail
list_name.pop(index)
list_name.sort()
list_name.reverse()
```

# Dictionaries
- Unordered mappings for storing objects

```
d = {'key1':'value1', 'key2':'value2'}
d['key1']
d.key()
d.values()
d.items()
```
