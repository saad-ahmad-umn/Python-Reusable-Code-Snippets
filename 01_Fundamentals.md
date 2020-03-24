# Fundamentals 


```python
# The Zen of Python, by Tim Peters
import this
```

>     The Zen of Python, by Tim Peters
>     
>     Beautiful is better than ugly.
>     Explicit is better than implicit.
>     Simple is better than complex.
>     Complex is better than complicated.
>     Flat is better than nested.
>     Sparse is better than dense.
>     Readability counts.
>     Special cases aren't special enough to break the rules.
>     Although practicality beats purity.
>     Errors should never pass silently.
>     Unless explicitly silenced.
>     In the face of ambiguity, refuse the temptation to guess.
>     There should be one-- and preferably only one --obvious way to do it.
>     Although that way may not be obvious at first unless you're Dutch.
>     Now is better than never.
>     Although never is often better than *right* now.
>     If the implementation is hard to explain, it's a bad idea.
>     If the implementation is easy to explain, it may be a good idea.
>     Namespaces are one honking great idea -- let's do more of those!
>



## Resources 

* Documentation: https://docs.python.org/3/
* Tutorials: http://www.tutorialspoint.com/python/python_variable_types.htm
* Built-in functions: https://docs.python.org/3/library/functions.html
* Python Module Index: https://docs.python.org/3/py-modindex.html
* PyPI - the Python Package Index: https://pypi.python.org/pypi


```python
#Core/Standard libraries in Python
import math
dir(math)[:15]
```

>
>     ['__doc__',
>      '__loader__',
>      '__name__',
>      '__package__',
>      '__spec__',
>      'acos',
>      'acosh',
>      'asin',
>      'asinh',
>      'atan',
>      'atan2',
>      'atanh',
>      'ceil',
>      'copysign',
>      'cos']
>




```python
# To learn more about a function
help(math.sin)
```

>     Help on built-in function sin in module math:
>     
>     sin(x, /)
>         Return the sine of x (measured in radians).
>


​    

## Reserved Words

| Key words |        |
| --------- | ------ |
| False     | class  |
| continue  | for    |
| from      | non    |
| global    | not    |
| or        | yield  |
| break     | except |




```python
import keyword
```


```python
# Check if a word is an identified Python keyword or not
print (keyword.iskeyword("print")) #
print (keyword.iskeyword("lambda")) #
```

>     False
>     True
>



```python
# All built-in identifiers of Python
dir(__builtins__)[:15]
```

>
>     ['ArithmeticError',
>      'AssertionError',
>      'AttributeError',
>      'BaseException',
>      'BlockingIOError',
>      'BrokenPipeError',
>      'BufferError',
>      'BytesWarning',
>      'ChildProcessError',
>      'ConnectionAbortedError',
>      'ConnectionError',
>      'ConnectionRefusedError',
>      'ConnectionResetError',
>      'DeprecationWarning',
>      'EOFError']
>



## Naming rules ##
* Syntax: (underscore or letter) + (any number of digits or underscores)
    * _rick is a good name
    * 2_rick is not
+ Case sensitive
    * Rick is different from rick
+ No Reserved words


```python
# Python is case sensitive. This returns false
"Saad" == 'saad'
```

>
>     False
>




```python
# Invalid variable names. Will get a syntax error when run
z_! = 1
```

>
>       File "<ipython-input-59-a0c45f0eb56d>", line 2
>         z_! = 1
>           ^
>     SyntaxError: invalid syntax
>




```python
# Invalid variable names. Will get a syntax error when run
2_x = 1
```

>
>       File "<ipython-input-60-7469d2cd1898>", line 2
>         2_x = 1
>          ^
>     SyntaxError: invalid token
>



Comments
-----
* One line comments begin with the pound (#) sign
+ Multiline comments are triple-quoted'''


```python
# comment line

print('Hi World!')  #line comment
"""
    more lines
    of comments
    ...
    ...
"""
x=10
x
```

>     Hi World!
>

>     10
>



## Assignment


```python
spam = 'Spam'              #basic assignments
spam, ham = 'yum','YUM'    #tuple assignment
spam = ham = 'lunch'       #multiple target - can be used
```


```python
x = y = z = 10
```


```python
# Variable c gets the concatenated string
c = "jhvj""hvjh"
c
```

>
>     'jhvjhvjh'
>




```python
x,y = (2,4)
print( x + y)
```

>     6
>



Dynamically typed language
-----

* data types
    * numeric, string, boolean, classes (list, tuple, range, dictionary, ...)


```python
x = "abc"
z = x
type(z)
```

>
>     str
>


```python
id(x)
```

>
>     2161356563936
>


```python
del x
```


```python
x
```

>
>     ---------------------------------------------------------------------------
>     
>     NameError                                 Traceback (most recent call last)
>     
>     <ipython-input-19-6fcf9dfbd479> in <module>
>     ----> 1 x
>

>
>     NameError: name 'x' is not defined
>



Newline terminates each statement
-----

No ;
\ for line Continuation



Indentation marks blocks
-----

No {} (if, for, while, and functions ...


```python
x = -1
if x > 8:
    print("A")
elif x > 6:
    print("B")
elif x > 2:
    print("C")
else:
    print("F")
```

>     F
>



Expressions
-----

* Numerical
* String
* Boolean
* Classes ... specific


```python
# Gives the quotient
10 // 3
```

>
>     3
>


```python
print(10 // 3)
print(10/3)
print('a' + '1')
print('a' / 'b')
```

>     3
>     3.3333333333333335
>     a1
>

>     ---------------------------------------------------------------------------
>     
>     TypeError                                 Traceback (most recent call last)
>     
>     <ipython-input-22-bcd4ddd9a007> in <module>
>           2 print(10/3)
>           3 print('a' + '1')
>     ----> 4 print('a' / 'b')
>

>
>     TypeError: unsupported operand type(s) for /: 'str' and 'str'
>



Simple conditionals
-----

if
else
elif
PASS -- empt Block

```python
x = 1
if x == 1:
    y = 1
    z = x + y
    print(z)
elif x == 2:
    y = 5
    print(x + y)
else:
    print('Hi')
```

>     2
>



```python
# Works on large numbers
x = 10000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000
x + 1
```

>
>     10000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001
>



Function definition
-----
with or without return


```python
# The modulus operator calculates the remainder
def remainder(a,b):
    ''' This is my first function'''
    q = a // b  # // is truncating division.
    r = a - q*b
    return r

print(remainder(10,3))
print(10%3)
```

>     1
>     1
>



```python
# Help works on user-defined functions as well
help(remainder)
```

>     Help on function remainder in module __main__:
>     
>     remainder(a, b)
>         This is my first function
>


```python
print(remainder('10','3'))
#print(remainder(10,3))
#print(10%3)
```

>     1
>

```python
def f(x,y):
    return x+y
```


```python
f('a','bc')
```

>
>     'abc'
>


```python
f(4,3)
```

>
>     7
>


```python
f([1,2,3],[4,5,6])
```

>
>     [1, 2, 3, 4, 5, 6]
>


```python
# one line function
f = lambda x, y: x + y
f(1,2)
```

>
>     3
>



The in keyword and case sensitive
-----

```python
var1 = 'this line is a test'
if 'Line' in var1:
    print("'" + var1 + "' has Line")
else:
    print("'" + var1 + "' does not have Line")
```

>     'this line is a test' does not have Line
>



Iterable containers | for...in...
-----

Any class can behave as a container that can be iterated through by implementing the special methods ( __iter__ and __next__)

* file
+ string
+ list
+ dictionary
+ range
+ tuple

```python
for j in (0,10,2):
    print(j+1)
```

>     1
>     11
>     3
>

```python
for char in "AbCdEf": 
    print(char+ ' ')
```

>     A 
>     b 
>     C 
>     d 
>     E 
>     f 
>

```python
x = 0
while x < 10:
    print(x)
    x = x + 1
print('done')
```

>     0
>     1
>     2
>     3
>     4
>     5
>     6
>     7
>     8
>     9
>     done
>



## User Input

* interactive request
* via command line

```python
x = input("What is your name:")
print('Your name is:' ,x)
```

>     What is your name:Saad
>     Your name is: Saad
>



## Casting


```python
#it return string type
#age = eval(input("How old are you?"))
age = input("How old are you?")
age10 = int(age) + 10
print('after 10 years, your age will be:%d' % (age10))
```

>     How old are you?29
>     after 10 years, your age will be:39
>

```python
2j * 3
```

>
>     6j
>


```python
10j / 2j
```

>
>     (5+0j)
>



## Standard libraries


```python
import random as rnd
dir(rnd)
#Use TAB
#Use Shift TAB
rnd.random()
```

>
>     0.24572618500197763
>


```python
help(sorted)
```

>     Help on built-in function sorted in module builtins:
>     
>     sorted(iterable, /, *, key=None, reverse=False)
>         Return a new list containing all items from the iterable in ascending order.
>         
>         A custom key function can be supplied to customize the sort order, and the
>         reverse flag can be set to request the result in descending order.
>


```python
import math
dir(math)[:15]
```

>
>     ['__doc__',
>      '__loader__',
>      '__name__',
>      '__package__',
>      '__spec__',
>      'acos',
>      'acosh',
>      'asin',
>      'asinh',
>      'atan',
>      'atan2',
>      'atanh',
>      'ceil',	
>      'copysign',
>      'cos']
>


```python
import math 
print(math.sin(20))
```

>     0.9129452507276277
>

