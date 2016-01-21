## [7kyu] Complementary DNA
### Details
```
Description:

Deoxyribonucleic acid (DNA) is a chemical found in the nucleus of cells and carries the "instructions" for the development and functioning of living organisms.

If you want to know more http://en.wikipedia.org/wiki/DNA

In DNA strings, symbols "A" and "T" are complements of each other, as "C" and "G". You have function with one side of the DNA (string, except for Haskell); you need to get the other complementary side. DNA strand is never empty or there is no DNA at all (again, except for Haskell).

DNA_strand ("ATTGC") # return "TAACG"

DNA_strand ("GTAT") # return "CATA"
```

### My solution
```
def DNA_strand(dna):
    return ''.join([{'A': 'T', 'T': 'A', 'G': 'C', 'C': 'G'}[c] for c in dna])
```

### Good case
```
import string
def DNA_strand(dna):
    return dna.translate(string.maketrans("ATCG","TAGC"))
    # Python 3.4 solution || you don't need to import anything :)
    # return dna.translate(str.maketrans("ATCG","TAGC"))
```

## [7kyu] Find the capitals
### Details
```
Write a function that takes a single string (word) as argument. The function must return an ordered list containing the indexes of all capital letters in the string.
```

### My solution
```
def capitals(word):
    result = []
    for index, str in enumerate(list(word)) :
        if str.isupper() :
            result.append(index)
                
    return result
```

### Good case
```
def capitals(word):
    return [i for (i, c) in enumerate(word) if c.isupper()]
```

## [7kyu] Money, Money, Money
### Details
```
Mr. Scrooge has a sum of money 'P' that wants to invest, and he wants to know how many years 'Y' this sum has to be kept in the bank in order for this sum of money to amount to 'D'.

The sum is kept for 'Y' years in the bank where interest 'I' is paid yearly, and the new sum is re-invested yearly after paying tax 'T'

Note that the principal is not taxed but only the year's accrued interest
```
### My solution
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

### Good case
```
from math import ceil, log

def calculate_years(principal, interest, tax, desired):
    if principal >= desired: return 0
    
    return ceil(log(float(desired) / principal, 1 + interest * (1 - tax)))
```
