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



# Statements
- If, Elif, Else
```
if some_condition:
    # execute some code
elif some_other_condition:
    # something different
else:
    # do sth else
```

# Loop
- for
- while
- range(a,b), range(a,b,step)
```
my_iterable = [1,2,3]
for item_name in my_iterable: # Get value
    print(item_name)

range(a,b) => return [a,b)

my_list = [(1,2), (3,4)]
for (a,b) in my_list:
    print(a,b)

d = {'k1':1,'k2':2,'k3':3}
for a in d.items():
    print(a)
for key,value in d.items():
    print(value)

while condition:
    #execution
else:
    #execution

x = [1,2,3]

for item in x:
    pass # Does nothing at all

print('end of my script')

break
continue

word = 'abcd';
The enumerate() function in Python simplifies looping by providing both the index and the value of an iterable.
for item in enumerate(word):
    print(item)
for index,item in enumerate(word):
    print(index)
    print(item)

mylist1 = [1,2]
mylist2 = ['a','b']
mylist3 = [100,200]

for item in zip(mylist1,mylist2,mylist3)
    print(item)

'x' in [1,2,3] #return false => type boolean

min(mylist1)
max(mylist2)

result = input('Type input here: ') #input return str => if want input as int => int(result), float(result)....
```

# List Comprehensions

```
[x for x in range(1,51) if x%3 == 0]
[x if x%2==0 else 'ODD' for x in range(0,11)]
[word[0] for word in st.split()]
[x*y for x in [2,4,6] for y in [1,10,100]]
```

# Methods, Function
- Medthods using object-oriented programming and classes
- Function - blocks of code
```
mylist.pop()
=> pop() = method
help(mylist.pop)


def name_of_function(name):
    """
    explain function
    """
    print("Hello " + name)

name_of_function("DDD")

def add_function(num1,num2):
    return num1+num2

result = add_function(1,2)

def say_hello(name='Jennie'):
    print(f'Hello {name},')
    print("How are you?")

say_hello()


### Unpacking tuple

stock_prices = [('APPL',200),('GOOG',400)]

def employee_check(stock_prices):
    current_max = 0
    employee_of_month = ''

    return (employee_of_month, current_max)

symbol, price = employee_check(stock_prices) #Unpacking
```
