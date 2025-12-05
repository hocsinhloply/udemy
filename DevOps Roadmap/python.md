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
```
print('The {} {} {}'.format('fox', 'brown', 'quick'))
print('The {2} {1} {0}'.format('fox', 'brown', 'quick'))
print('The {0} {0} {0}'.format('fox', 'brown', 'quick'))
print('The {f} {b} {b}'.format(f='fox', b='brown', q='quick'))
print("The result was {r:1.3f}".format(r=result))
print("The result was {r:10.3f}".format(r=result))
print(f'Hello, his name is {name}') # F strings
```

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

# Tuples
- Same lists but **Immutability**
- Use ()

- Two methods associated with count(), index('')
```
t = ('a', 'a', 'b')
t.count('a')
t.index('a') return first time 'a' appear
```

# Sets
- unique elements
- unordered

```
myset = set()
myset.add(1)
```

# Booleans
- True or False statements

```
True or False not true, false
```
# I/O with Basic Files in Python (.txt)

```
%%writefile myfile.txt #save in the same location
Hello this is a text file
this is the second line

myfile = open('myfile.txt')

pwd #check working location

myfile.read() #read to end file and cursor point at end => myfile.read() = '' => need reset cursor myfile.seek({index})
myfile.seek(0) # reset at begin
myfile.readlines() #return list each lines
myfile.close()

with open('myfile.txt') as my_new_file:
  contents = my_new_file.read()

with open('myfile.txt') as my_new_file:
  contents = my_new_file.read()
## shift tab open(herehere'myfile.txt') => open information for function
Window path format: "C:\\User\\test.txt"
MacOS, Linux: "/Users/YouUserName/test.txt"
```
# Comparison Operators

For the following quiz questions, we will get a preview of comparison operators. In the table below, a=3 and b=4.

<table class="table table-bordered">
<tr>
<th style="width:10%">Operator</th><th style="width:45%">Description</th><th>Example</th>
</tr>
<tr>
<td>==</td>
<td>If the values of two operands are equal, then the condition becomes true.</td>
<td> (a == b) is not true.</td>
</tr>
<tr>
<td>!=</td>
<td>If values of two operands are not equal, then condition becomes true.</td>
<td> (a != b) is true.</td>
</tr>
<tr>
<td>&gt;</td>
<td>If the value of left operand is greater than the value of right operand, then condition becomes true.</td>
<td> (a &gt; b) is not true.</td>
</tr>
<tr>
<td>&lt;</td>
<td>If the value of left operand is less than the value of right operand, then condition becomes true.</td>
<td> (a &lt; b) is true.</td>
</tr>
<tr>
<td>&gt;=</td>
<td>If the value of left operand is greater than or equal to the value of right operand, then condition becomes true.</td>
<td> (a &gt;= b) is not true. </td>
</tr>
<tr>
<td>&lt;=</td>
<td>If the value of left operand is less than or equal to the value of right operand, then condition becomes true.</td>
<td> (a &lt;= b) is true. </td>
</tr>
</table>
