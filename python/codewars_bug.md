## Snakes and Camels
http://www.codewars.com/kata/snakes-and-camels/train/python

##### Details
```
Snakes and Camels

CamelCase and snake_case are two of the most common ways phrases and names are represented in programming langauges, convention and preference often being the deciding factor on whichever one should be used. But if we ever run into a situation where we need to have both, we really should be able to convert between them.

So this Kata should be simple enough; you've got to implement two functions: toCamelCase() and toSnakeCase(). (For the purposes of these challenges, we'll be using UpperCamelCase).

So, let's set down a couple of rules (by example) of how the functions behave.

  original  |  toCamelCase  |  toSnakeCase
 ------------------------------------------

    'foo'         'Foo'           'foo'
    'Foo'         'Foo'           'foo'
    'FOO'         'Foo'           'foo'

  'FooBar'       'FooBar'       'foo_bar'
  'foo_bar'      'FooBar'       'foo_bar'
  'FOO_BAR'      'FooBar'       'foo_bar'
  'FOO_bar'      'FooBar'       'foo_bar'

  'foo bar'      'FooBar'       'foo_bar'
  'foo.bar'      'Foo.Bar'      'foo.bar'
  'foo::bar'     'Foo::Bar'     'foo::bar'
  'FOO::Bar'     'Foo::Bar'     'foo::bar'
```

##### My solution
문제 테스트 케이스 안돌아가고 뭔가 이상하다.
나중에 다시 풀어본다.
```
def to_camel_case(string_):
    if not string_:
        return ''
        
    r = list(string_)
    c = True
    for x in r:
        if c:
            r.append(x.upper())
        elif not x.isalpha():
            c = True
        else:
            if c:
                r.append(x.upper())
                c = False
            else:
                r.append(x)
    return ''.join(r)
    
def to_snake_case(string_):
    if not string_:
        return ''
    string_ = string_.strip()
    r = []
    wasLower = False
    wasAlpha = False
    wasDigit = False
    
    for i, x in enumerate(string_):
        print "[%s][%s][%s]" % (i, x, ord(x))
        if i and wasLower and wasAlpha and x.isupper():
            r.append('_' + x.lower())
        elif i and (i + 1) < len(string_) and wasAlpha and x.isupper() and string_[i+1].islower():
            r.append('_' + x.lower())
        elif i and wasDigit and x.isalpha():
            r.append('_' + x.lower())
        elif x.isspace():
                r.append('_')
        else:
            r.append(x.lower())
            
        wasLower = x.islower()
        wasAlpha = x.isalpha()
        wasDigit = x.isdigit()
        
    return ''.join(r)
```
