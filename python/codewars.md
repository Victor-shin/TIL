## Insert dashes
##### Details
```
Write a function insertDash(num) that will insert dashes ('-') between each two odd numbers in num. For example: if num is 454793 the output should be 4547-9-3. Don't count zero as an odd number.
```

##### My solution
```
import re

def insert_dash(num):
    p = re.compile(r'(1|3|5|7|9)(1|3|5|7|9)')
    return re.sub(p, r'\1-\2', re.sub(p, r'\1-\2', str(num)))
```

##### Good case
```
import re

def insert_dash(num):
    return re.sub(r'([13579])(?=[13579])', r'\1-', str(num))
```

##### Good case
```
def insert_dash(num):
    def odd(c):
        return not (ord(c) & 1 ^ 1)
    a = []
    for digit in str(num):
        if odd(digit) and a and odd(a[-1]):
            a.append('-')
        a.append(digit)
    return "".join(a)
```

## Flattening Lists
##### Details
```
In this Kata you will create a function that takes a list of lists as an input and returns a flat list.
```

##### My solution (Good case)
```
def flatten(l):
  return [item for sublist in l for item in sublist]
```

##### Good case
```
from itertools import chain

def flatten(l):
  return list(chain(*l))
```

## Find the next perfect square!
##### Details
```
Description:

You might know some pretty large perfect squares. But what about the NEXT one?

Complete the findNextSquare method that finds the next integral perfect square after the one passed as a parameter. Recall that an integral perfect square is an integer n such that sqrt(n) is also an integer.

If the parameter is itself not a perfect square, than -1 should be returned. You may assume the parameter is positive.

Examples:

findNextSquare(121) --> returns 144
findNextSquare(625) --> returns 676
findNextSquare(114) --> returns -1 since 114 is not a perfect
```

##### My solution
```
from math import sqrt
def find_next_square(sq):
    return (sqrt(sq)+1)**2 if sqrt(sq)%1 == 0 else -1
```

##### Good case
```
from math import sqrt
def find_next_square(sq):
    return (sqrt(sq)+1)**2 if sqrt(sq)%1 == 0 else -1
```

## Invisible cubes
##### Details
```
Imagine there's a big cube consisting of n^3 small cubes. Calculate, how many small cubes are not visible from outside.

For example, if we have a cube which has 4 cubes in a row, then the function should return 8, because there are 8 cubes inside our cube (2 cubes in each dimension)
```

##### My solution
```
def not_visible_cubes(n):
    return 0 if n < 3 else pow(n - 2, 3)
```

##### Good case
```
def not_visible_cubes(n):
    return max(n - 2, 0) ** 3
```

## Credit Card Validifier
##### Details
```
Make a program that sees if a credit card number is valid or not. Also the program should tell you what type of credit card it is if it is valid.

The five things you should consider in your program is: AMEX, Discover, VISA, Master, and Invalid

Discover starts with 6011 and has 16 digits, AMEX starts with 34 or 37 and has 15 digits, Master Card starts with 51-55 and has 16 digits, VISA starts with 4 and has 13 or 16 digits.

Ex: Input: 6011364837263748 --> Output: "Discover" Ex: Input: 5318273647283745 --> Output: "MasterCard" Ex: Input: 12345678910 --> Output: "Invalid" Ex: Input: 371236473823676 --> Output: "AMEX" Ex: Input: 4128374839283 --> Output: "VISA"

```

##### My solution
```
def credit(num):
    if not str(num).isdigit():
        return "Invalid"
        
    rules = [
        ('Discover', [16], ('6011')),
        ('AMEX', [15], ('34', '37')),
        ('MasterCard', [16], ('51', '52', '53', '54', '55')),
        ('VISA', [13, 16], ('4'))
    ]
    
    s = str(num)
    l = len(s)
    for rule in rules:
        if l in rule[1] and s.startswith(rule[2]):
            return rule[0]
    
    return "Invalid"
```

##### Good case #1
```
import re

def credit(num):
    num = str(num)
    if re.search(r'^6011\d{12}$', num):
        return 'Discover'
    elif re.search(r'^(34|37)\d{13}$', num):
        return 'AMEX'
    elif re.search(r'^5[1-5]\d{14}$', num):
        return 'MasterCard'
    elif re.search(r'^4(\d{12}|\d{15})$', num):
        return 'VISA'
    else:
        return "Invalid"
```

##### Good case #2
```
def credit(num):
    if str(num).startswith('6011') and len(str(num)) == 16:
        return 'Discover'
    elif str(num).startswith(('34', '37')) and len(str(num)) == 15:
        return 'AMEX'
    elif str(num).startswith(('51', '52', '53', '54', '55')) and len(str(num)) == 16:
        return 'MasterCard'
    elif str(num).startswith('4') and (len(str(num)) == 13 or len(str(num)) == 16):
        return 'VISA'
    return 'Invalid'
```

##### Sample unittest
```
#!/usr/bin/python

import re
import unittest

class Credit():
    def credit(self, num):
        discover = re.compile("^6011[0-9]{12}$")
        amex = re.compile("^(34|37)\d{13}$")
        master = re.compile("^5[1-5]\d{14}")
        visa = re.compile("^4\d{12,15}$")

        #if (discover.search(str(num)) != None):
        if (discover.search(str(num))):
            return "Discover"
        elif (amex.search(str(num))):
            return "AMEX"
        elif (master.search(str(num))):
            return "MasterCard"
        elif (visa.search(str(num))):
            return "VISA"
        else:
            return "Invalid"

class Test(unittest.TestCase):
    def test_credit(self):
        c = Credit()
        self.assertEquals(c.credit(6011364837263748), "Discover")
        self.assertEquals(c.credit(5318273647283745), "MasterCard")
        self.assertEquals(c.credit(12345678910), "Invalid")
        self.assertEquals(c.credit(371236473823676), "AMEX")
        self.assertEquals(c.credit(4128374839283), "VISA")
        self.assertEquals(c.credit(6011253648736259), "Discover")
        self.assertEquals(c.credit(6011728364710763), "Discover")
        self.assertEquals(c.credit(341627384637453), "AMEX")
        self.assertEquals(c.credit(371628394536298), "AMEX")
        self.assertEquals(c.credit(1739712491524), "Invalid")
        self.assertEquals(c.credit(12984580723695), "Invalid")
        self.assertEquals(c.credit(5117283748253647), "MasterCard")
        self.assertEquals(c.credit(4142593846732), "VISA")
        self.assertEquals(c.credit(5417283945362734), "MasterCard")
        self.assertEquals(c.credit(4152637483526371), "VISA")

if __name__ == '__main__':
    unittest.main()
```

## Invalid Input - Error Handling #1
##### Details
```
Error Handling is very important in coding. Most error handling seems to be overlooked or not implemented properly.
Task

Your task is to implement a function which is expected to take a string and return an object containing the properties vowels and consonants The vowels property must contain the total count of vowels ('y' in this case is not a vowel), and consonants are any other letters, you must also trim any spaces. Don't forget to handle invalid input, though you must always return valid output.
```

##### My solution
```
def get_count(words = ''):
    v, c = 0, 0
    if type(words) in (str, unicode) and len(words):
        v = len([x for x in words if x.isalpha() and x.lower() in 'aeiou'])
        c = len([x for x in words if x.isalpha() and x.lower() not in 'aeiou'])
        
    return {'vowels': v, 'consonants': c}
```

##### Good case
```
def get_count(words=""):
    if not isinstance(words, str):
        return {'vowels':0,'consonants':0}
    letter = "".join([c.lower() for c in words if c.isalpha()])
    vowel = "".join([c for c in letter if c in 'aeiou'])
    consonant = "".join([c for c in letter if c not in 'aeiou']) 
    return {'vowels':len(vowel),'consonants':len(consonant)}
```
    
## Sum of numerous arguments
##### Details
```
After calling the function findSum() with any number of non-negative integer arguments, it should return the sum of all those arguments. If no arguments are given, the function should return 0, if negative arguments are given, it should return -1.

eg

find_sum(1,2,3,4); # returns 10 
find_sum(1,-2);    # returns -1 
find_sum();        # returns 0
Hint: research the arguments object on google or read Chapter 4 from Eloquent Javascript
```

##### My solution
```
def find_sum(*args):
    sum = 0
    for i in args:
        sum += i
        if i < 0 : 
            return -1
        
    return sum
```

##### Good case
```
def find_sum(*args):
    return -1 if any(x < 0 for x in args) else sum(args)
```

## [7kyu] Complementary DNA
##### Details
```
Description:

Deoxyribonucleic acid (DNA) is a chemical found in the nucleus of cells and carries the "instructions" for the development and functioning of living organisms.

If you want to know more http://en.wikipedia.org/wiki/DNA

In DNA strings, symbols "A" and "T" are complements of each other, as "C" and "G". You have function with one side of the DNA (string, except for Haskell); you need to get the other complementary side. DNA strand is never empty or there is no DNA at all (again, except for Haskell).

DNA_strand ("ATTGC") # return "TAACG"

DNA_strand ("GTAT") # return "CATA"
```

##### My solution
```
def DNA_strand(dna):
    return ''.join([{'A': 'T', 'T': 'A', 'G': 'C', 'C': 'G'}[c] for c in dna])
```

##### Good case
```
import string
def DNA_strand(dna):
    return dna.translate(string.maketrans("ATCG","TAGC"))
    # Python 3.4 solution || you don't need to import anything :)
    # return dna.translate(str.maketrans("ATCG","TAGC"))
```

## [7kyu] Find the capitals
##### Details
```
Write a function that takes a single string (word) as argument. The function must return an ordered list containing the indexes of all capital letters in the string.
```

##### My solution
```
def capitals(word):
    result = []
    for index, str in enumerate(list(word)) :
        if str.isupper() :
            result.append(index)
                
    return result
```

##### Good case
```
def capitals(word):
    return [i for (i, c) in enumerate(word) if c.isupper()]
```

## [7kyu] Money, Money, Money
##### Details
```
Mr. Scrooge has a sum of money 'P' that wants to invest, and he wants to know how many years 'Y' this sum has to be kept in the bank in order for this sum of money to amount to 'D'.

The sum is kept for 'Y' years in the bank where interest 'I' is paid yearly, and the new sum is re-invested yearly after paying tax 'T'

Note that the principal is not taxed but only the year's accrued interest
```
##### My solution
```
def calculate_years(principal, interest, tax, desired, year = 0):
    if principal == desired :
        return 0

    while principal < desired :
        year += 1        
        yi = principal * interest
        yt = yi * tax

        principal += (yi - yt)    

    return year
```

##### Good case
```
from math import ceil, log

def calculate_years(principal, interest, tax, desired):
    if principal >= desired: return 0
    
    return ceil(log(float(desired) / principal, 1 + interest * (1 - tax)))
```
