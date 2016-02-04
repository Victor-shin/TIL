## Find primes
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
