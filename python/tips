## TIP

##### timeit.Timer
timeit.Timer 라는 것도 있구나 ~
좋구나 ~
https://docs.python.org/2/library/timeit.html
```
>>> timeit.Timer(
...         'reduce(lambda x,y: x+y,l)',
...         'l=[[1, 2, 3], [4, 5, 6, 7, 8], [1, 2, 3, 4, 5, 6, 7]] * 10'
...     ).timeit()
13.073173999786377
>>> timeit.Timer(
...         '[item for sublist in l for item in sublist]',
...         'l=[[1, 2, 3], [4, 5, 6, 7, 8], [1, 2, 3, 4, 5, 6, 7]] * 10'
...     ).timeit()

7.3597259521484375
>>> timeit.Timer(
...         'sum(l, [])',
...         'l=[[1, 2, 3], [4, 5, 6, 7, 8], [1, 2, 3, 4, 5, 6, 7]] * 10'
...     ).timeit()
9.677650928497314
```

##### startswith에 tuple이 올 수 있다! 
