## 7kyu Money, Money, Money
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
