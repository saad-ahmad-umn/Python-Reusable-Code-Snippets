
# Python Regular Expressions
* matching/extracting text patterns

https://www.debuggex.com/cheatsheet/regex/python

## Basic Patterns
* a, X, 9, < -- ordinary characters just match themselves exactly.  
* . (a period) -- matches any single character except newline '\n'
* \w -- (lowercase w) matches a "word" character: a letter or digit or underbar [a-zA-Z0-9_]. Note that although "word" is the mnemonic for this, it only matches a single word char, not a whole word. \W (upper case W) matches any non-word character.
* \b -- boundary between word and non-word
* \s -- (lowercase s) matches a single whitespace character -- space, newline, return, tab, form [ \n\r\t\f]. \S (upper case S) matches any non-whitespace character.
* \t, \n, \r -- tab, newline, return
* \d -- decimal digit [0-9] (some older regex utilities do not support but \d, but they all support \w and \s)
* ^ = start, $ = end -- match the start or end of the string
* \ -- inhibit the "specialness" of a character. So, for example, use \. to match a period or \\ to match a slash. If you are unsure if a character has special meaning, such as '@', you can put a slash in front of it, \@, to make sure it is treated just as a character.

##### The meta-characters which do not match themselves: . ^ $ * + ? { [ ] \ | ( )

## Repetition
* '+' -- 1 or more occurrences of the pattern to its left, e.g. 'i+' = one or more i's
* '*' -- 0 or more occurrences of the pattern to its left
* '?' -- match 0 or 1 occurrences of the pattern to its left


```python
import re
regex = r"[a-zA-Z]+ \d\d"
matches = re.findall(regex, "June 24, August 9, Dec 12")
for match in matches:
    print(match)
matches
```

>     June 24
>     Dec 12
>

>     ['June 24', 'Dec 12']
>

```python
regex = r"([a-zA-Z]+) \d+"
matches = re.findall(regex, "June 24, August 9, Dec 12")
for match in matches:
    print(match)
matches
```

>     June
>     August
>     Dec
>

>     ['June', 'August', 'Dec']
>


```python
import re
match = re.search(r'e..o', 'Hello World!')
match.group()

```

>
>     'ello'
>


```python
match = re.search(r'World', 'Hello World!') 
match.group()
```

>
>     'World'
>


```python

## . = any char but \n
match = re.search(r'..d', 'Hello World!') 
match.group()
```

>
>     'rld'
>


```python
## \d = digit char, \w = word char
match = re.search(r'\d\d', 'p123g and 654is a number') 

match.group()


```

>
>     '12'
>


```python
# world of length 3
match = re.search(r'\w\w\w', '@@abcd!!')
match.group()
```

>
>     'abc'
>



## findall

* The single most powerful function in the re module


```python
## Suppose we have a text with many email addresses
str = 'purple alice@google.com, blah monkey bob@abc.com blah dishwasher'

## Here re.findall() returns a list of all the found email strings
emails = re.findall(r'[\.\w]+@[\w\.]+', str) ## ['alice@google.com', 'bob@abc.com']
emails
```

>
>     ['alice@google.com', 'bob@abc.com']
>


```python
str = 'purple alice@google.com, blah monkey bob@abc.com blah dishwasher'
tuples = re.findall(r'([\w\.]+)@([\w\.]+com)', str)
tuples  ## [('alice', 'google.com'), ('bob', 'abc.com')]
```

>
>     [('alice', 'google.com'), ('bob', 'abc.com')]
>


```python
phonePattern = re.compile(r'^(\d{3})\D*(\d{3})\D*(\d{4})\D*(\d*)$')
phonePattern.search('80055512121234').groups()
```

>
>     ('800', '555', '1212', '1234')
>


```python
phonePattern.search('800.555.1212 x1234').groups()
```

>
>     ('800', '555', '1212', '1234')
>


```python
phonePattern.search('800-555-1212').groups()
```

>
>     ('800', '555', '1212', '')
>


