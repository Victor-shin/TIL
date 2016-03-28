## TIP
##### Simple logger
- Link
https://docs.python.org/2/howto/logging.html

- How to
```
import logging
logging.basicConfig(filename="/tmp/testpython.log", format="%(asctime)s [%(levelname)s] %(message)s", datefmt='%m/%d/%Y %H:%M:%S', level=logging.DEBUG)
logging.error("test")
```
- Output
```
trknight78@sinhyeon-yong-ui-MacBook-Pro:/tmp » tail -f testpython.log
03/28/2016 13:31:36 [ERROR] test
```

##### python 스러운 문법이 뭐가 있을까? 계속 정리해보자
- expression if expression else expression
- 다음 URL 참고. (좋다)
http://docs.python-guide.org/en/latest/writing/style/

##### timeit.Timer
성능측정함수. timeit()에 횟수를 명시하지 않으면 디폴트로 1,000,000회 반복한다.
(timeit.Timer 라는 것도 있구나 ~ 좋구나 ~)
- https://docs.python.org/2/library/timeit.html

- 로컬에서(victor.shin macbook pro) 돌린 결과
  - lambda
  ```
>>> timeit.Timer(
...         'reduce(lambda x,y: x+y,l)',
...         'l=[[1, 2, 3], [4, 5, 6, 7, 8], [1, 2, 3, 4, 5, 6, 7]] * 10'
...     ).timeit()
13.073173999786377
```
  - nested loop
  ```
>>> timeit.Timer(
...         '[item for sublist in l for item in sublist]',
...         'l=[[1, 2, 3], [4, 5, 6, 7, 8], [1, 2, 3, 4, 5, 6, 7]] * 10'
...     ).timeit()

7.3597259521484375
```
  - sum
  ```
>>> timeit.Timer(
...         'sum(l, [])',
...         'l=[[1, 2, 3], [4, 5, 6, 7, 8], [1, 2, 3, 4, 5, 6, 7]] * 10'
...     ).timeit()
9.677650928497314
```

##### String type
str.startswith()의 파라미터로 tuple이 올 수 있다! 

#### REGEXP
(?= re)	Specifies position using a pattern. Doesn't have a range.
```
import re

def insert_dash(num):
    return re.sub(r'([13579])(?=[13579])', r'\1-', str(num))
```
"13579"를 넣으면 "1-3-5-7-9"로 나온다.

#### divmod : return a pair of numbers consisting of their quotient and remainder

#### Get all subset
```python
from itertools import combinations, chain
allsubsets = lambda n: list(chain(*[combinations(range(n), ni) for ni in range(n+1)]))
```
