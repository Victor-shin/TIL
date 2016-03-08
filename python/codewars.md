## [6kyu] Playing with digits
##### Details
```
Some numbers have funny properties. For example:

89 --> 8¹ + 9² = 89 * 1

695 --> 6² + 9³ + 5⁴= 1390 = 695 * 2

46288 --> 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
Given a positive integer n written as abcd... (a, b, c, d... being digits) and a positive integer p we want to find a positive integer k, if it exists, such as the sum of the digits of n taken to the successive powers of p is equal to k * n. In other words:

Is there an integer k such as : (a ^ p + b ^ (p+1) + c ^(p+2) + d ^ (p+3) + ...) = n * k
If it is the case we will return k, if not return -1.

Note: n, p will always be given as strictly positive integers.

dig_pow(89, 1) should return 1 since 8¹ + 9² = 89 = 89 * 1
dig_pow(92, 1) should return -1 since there is no k such as 9¹ + 2² equals 92 * k
dig_pow(695, 2) should return 2 since 6² + 9³ + 5⁴= 1390 = 695 * 2
dig_pow(46288, 3) should return 51 since 4³ + 6⁴+ 2⁵ + 8⁶ + 8⁷ = 2360688 = 46288 * 51
```

##### My solution
```
def dig_pow(n, p):
    (r, m) = divmod(sum([int(x)**(p + i) for i, x in enumerate(list(str(n)))]), n)
    return r if not m else -1
```

##### Good solution
```
def dig_pow(n, p):
    k, fail = divmod(sum(int(d)**(p + i) for i, d in enumerate(str(n))), n)
    return -1 if fail else k
```

## [7kyu] Colour Association
##### Details
```
Colour plays an important role in our lifes. Most of us like this colour better then another. User experience specialists believe that certain colours have certain meanings for us psycologically.

You are given a two dimentional array, composed of a colour and its 'common' association in each array element. The function you will write needs to return the colour as 'key' and association as its 'value'.

For example: var array = ["white", "goodness"] => {white: 'goodness'}
```

##### My solution
```
def colour_association(arr):
    return [{k : v} for k, v in arr]
```

##### Good case
```
def colour_association(arr):
    return [{k: v} for k, v in arr]
```

## [7kyu] Binary scORe
##### Details
```
Given a number n we will define it's scORe to be 0 | 1 | 2 | 3 | ... | n, where | is the bitwise OR operator.

Write a function that takes n and finds it's scORe.

Examples

n	scORe n
0	0
1	1
49	63
1000000	1048575
```

##### My solution
```python
def score(n):
    if n < 2 :
        return n
        
    b, r = 0, 0
    while (1 << b) < n :
        r += pow(2, b)
        b += 1
    
    return r
```

##### Good case
```python
score=lambda n:2**n.bit_length()-1
```

## [Beta] Quicksum
##### Details
```
Description:

A checksum is an algorithm that scans a packet of data and returns a single number. The idea is that if the packet is changed, the checksum will also change, so checksums are often used for detecting transmission errors, validating document contents, and in many other situations where it is necessary to detect undesirable changes in data.

For this problem, you will implement a checksum algorithm called Quicksum. A Quicksum packet allows only uppercase letters and spaces. It always begins and ends with an uppercase letter.

Otherwise, spaces and uppercase letters can occur in any combination, including consecutive spaces.

A Quicksum is the sum of the products of each character’s position in the packet times the character’s value. A space has a value of zero, while letters have a value equal to their position in the alphabet.

So, A = 1, B = 2, etc., through Z = 26. Here are example Quicksum calculations for the packets “ACM” and “A C M”:

 
  
ACM
1 × 1 + 2 × 3 + 3 × 13 = 46 

A C M
1 x 1 + 3 x 3 + 5 * 13 = 75

When the packet doesn't have only uppercase letters and spaces or just spaces the result to quicksum have to be zero (0).
```

##### My solution
```
def quicksum(packet):
    return sum([((x[0] + 1) * (ord(x[1]) - 64)) for x in enumerate(packet) if x[1] != ' ']) if all ([x == ' ' or (x >= 'A' and x<= 'Z') for x in packet]) else 0
```

#### Good case
```
from string import ascii_uppercase

AZ = dict(zip(' ' + ascii_uppercase, xrange(27)))


def quicksum(packet):
    result = 0
    for i, a in enumerate(packet, 1):
        try:
            result += AZ[a] * i
        except KeyError:
            return 0
    return result
```

## [7kyu] Triangular Treasure
##### Details
```
Triangular numbers are so called because of the equilateral triangular shape that they occupy when laid out as dots. i.e.

1st (1)   2nd (3)    3rd (6)
*          **        ***
           *         **
                     *
You need to return the nth triangular number. You should return 0 for out of range values:

  triangular(0)==0,
  triangular(2)==3,
  triangular(3)==6,
  triangular(-10)==0
```

##### My Solution
```
def triangular(n):
    return 0 if n < 0 else n*(n+1)/2
```

##### Good case
```
def triangular(n):
    return n*(n+1)/2 if n > 0 else 0
```

## [7kyu] Remove the minimum
##### Details
```
The museum of incredible dull things

The museum of incredible dull things wants to get rid of some exhibitions. Miriam, the interior architect, comes up with a plan to remove the most boring exhibitions. She gives them a rating, and then removes the one with the lowest rating.

However, just as she finished rating all exhibitions, she's off to an important fair, so she asks you to write a program that tells her the ratings of the items after one removed the lowest one. Fair enough.

Task

Given an array of integers, remove the smallest value. If there are multiple elements with the same value, remove the one with a lower index. If you get an empty array/list, return an empty array/list.

Don't change the order of the elements that are left.

Examples

remove_smallest([1,2,3,4,5]) = [2,3,4,5]
remove_smallest([5,3,2,1,4]) = [5,3,2,4]
remove_smallest([2,2,1,2,1]) = [2,2,2,1]
```

##### My solution
```python
def remove_smallest(numbers):
    if not numbers:
        return numbers

    mi, mn = 0, numbers[0]
    for i, n in enumerate(numbers):
        if mn > n:
            mi, mn = i, n
        
    numbers.pop(mi)
    
    return numbers
```

##### Good case
```python
def remove_smallest(numbers):
    if numbers:
        numbers.remove(min(numbers))
    return numbers
```

## [6kyu] Number Shortening Filter
##### Details
```
Ok, here is a new one that they asked me to do with an interview/production setting in mind.

You might know and possibly even Angular.js; among other things, it lets you create your own filters that work as functions you put in your pages to do something specific to her kind of data, like shortening it to display it with a more concise notation.

In this case, I will ask you to create a function which return another function (or process, in Ruby) that shortens numbers which are too long, given an initial arrays of values to replace the Xth power of a given base; if the input of the returned function is not a numerical string, it should return the input itself as a string.

An example which could be worth more than a thousand words:

filter1 = shorten_number(['','k','m'],1000)
filter1('234324') == '234k'
filter1('98234324') == '98m'
filter1([1,2,3]) == '[1,2,3]'
filter2 = shorten_number(['B','KB','MB','GB'],1024)
filter2('32') == '32B'
filter2('2100') == '2KB';
filter2('pippi') == 'pippi'
If you like to test yourself with actual work/interview related kata, please also consider this one about building a breadcrumb generator
```

##### My solution
```python
def shorten_number(suffixes, base):
    l = len(suffixes)
    
    def operator(p):
        if not str(p).isdigit() : 
            return str(p)
            
        i, n = 0, int(p)   
        while n > base and (i + 1) < l:
            i, n = (i + 1), (n / base)

        return "{}{}".format(n, suffixes[i])

    return operator
```

##### Good case
```python
from math import log

def shorten_number(ar, base):
    def modifier(s):
        try:
            n = int(s)
            i = min(int(log(n, base)), len(ar)-1)
            
            return str(n / base ** i) + ar[i]
        except (TypeError, ValueError):
            return str(s)
    return modifier
```


## Clock in Mirror
##### Details
```
Peter can see a clock in the mirror from the place he sits in the office. When he saw the clock shows 12:22
He knows that the time is 11:38

in the same manner:
05:25 --> 06:35
01:50 --> 10:10
11:58 --> 12:02
12:01 --> 11:59

Please complete the method which is provided with mirror time as string, and return the real time as string.
```

##### My solution
```python
from datetime import datetime

def what_is_the_time(time_in_mirror):
    t = datetime.strptime("12:00", "%H:%M") - datetime.strptime(time_in_mirror, "%H:%M")
    h = (t.seconds / 3600) % 12
    m = (t.seconds / 60) % 60

    return "{:02}:{:02}".format(12 if h == 0 else h, m)
```

##### Good case
```python
def what_is_the_time(time_in_mirror):
    h, m = map(int, time_in_mirror.split(':'))
    return '{:02}:{:02}'.format(-(h + (m != 0)) % 12 or 12, -m % 60)
```

## The Most Amicable of Numbers
##### Details
```
Amicable numbers are two different numbers so related that the sum of the proper divisors of each is equal to the other number. (A proper divisor of a number is a positive factor of that number other than the number itself. For example, the proper divisors of 6 are 1, 2, and 3.)

For example, the smallest pair of amicable numbers is (220, 284); for the proper divisors of 220 are 1, 2, 4, 5, 10, 11, 20, 22, 44, 55 and 110, of which the sum is 284; and the proper divisors of 284 are 1, 2, 4, 71 and 142, of which the sum is 220.

Derive function amicableNumbers(num1, num2) which returns true/True if pair num1 num2 are amicable, false/False if not.
```

##### My solution
```python
def amicable_numbers(n1,n2):
    def sum_divisor(n):
        return sum([x for x in range(1, n) if not (n % x)])
        
    return sum_divisor(n1) == n2 and n1 == sum_divisor(n2)
```

##### Good case
```python
def proper_divisors_sum(n):
    return sum(a for a in xrange(1, n) if not n % a)


def amicable_numbers(a, b):
    return proper_divisors_sum(a) == b and proper_divisors_sum(b) == a
```


## String chunks
##### Details
```
Description:

You should write a function that takes a string and a positive integer n, splits the string into parts of n length and returns them in an array. It is ok for the last element to have less characters than n.

If n is not a valid size(> 0) (or is absent), you should return an empty array.

If n is greater than the lenght of the string, you should return an array with the only element being the same string.

Examples:

string_chunk('codewars', 2) # ['co', 'de', 'wa', 'rs']
string_chunk('thiskataeasy', 4) # ['this', 'kata', 'easy']
string_chunk('hello world', 3) # ['hel', 'lo ', 'wor', 'ld']
string_chunk('sunny day', 0) # []
```

##### My solution
```
def string_chunk(string, n = 0):
    if n <= 0 or type(n) is not int:
        return []
        
    r = []
    s = []
    l = len(string)
    for i, c in enumerate(string):
        s.append(c)
        if len(s) == n or i+1 == l:
            r.append(''.join(s))
            s = []

    return r
```

##### Good case
```
def string_chunk(string, n=0):
    return [string[i:i+n] for i in xrange(0,len(string), n)] if isinstance(n, int) and n > 0 else []
```

## [7kyu] Are there doubles?
##### Details
```
Your job is to build a function which determines whether or not there are double characters in a string (including whitespace characters). For example aa, !! or .

You want the function to return true if the string contains double characters and false if not.

Examples:

  double_check("abca")
  #returns False

  double_check("aabc")
  #returns True

  double_check("a 11 c d")
  #returns True

  double_check("AabBcC")
  #returns True

  double_check("a b  c")
  #returns True

  double_check("a b c d e f g h i h k")
  #returns False

  double_check("2020")
  #returns False

  double_check("a!@€£#$%^&*()_-+=}]{[|\"':;?/>.<,~")
  #returns False
```

##### My solution
```
def double_check(string):
    return any(x.lower() == string[i+1].lower() for i, x in enumerate(string[:-1]))
```

##### Good case
```
def double_check(str):
    return bool(re.search(r"(.)\1", str.lower()))
```

```
def double_check(inp):
    inp = inp.lower()
    return any(i == j for i, j in zip(inp[:-1], inp[1:]))
```

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
