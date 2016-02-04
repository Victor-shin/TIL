## Find primes
##### URL
http://www.codewars.com/kata/5681bc8d17af37f50e000015/train/javascript

##### Details
```
Your task is to take a given range and return an array of the prime numbers in that range.

You will write a function with the following parameters:

start is the integer from which your range starts.

end is the integer at which your range ends.

If the range does not contain any prime numbers return null.

Examples:

You can assume that parameters numbers will be positive integers and that the start of the range will be less than the end of the range.
```

##### My solution
자바 스크립트 버전 문제인지 모르고 python으로 풀어봄.
```
#!/usr/bin/python

def find_prime(start, end):
    def is_prime(num):
        if num == 1:
            return False
        if num == 2:
            return True

        for y in range(2, x):
            if num % y == 0:
                return False
        return True


    result = []
    for x in range(start, end + 1):
        if is_prime(x):
            result.append(x)

    return result

if __name__ == '__main__':
    print(find_prime(2, 10))
```
