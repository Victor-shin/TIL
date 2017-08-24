## UTIL
##### 두 날짜를 입력받고, 날짜 리스트를 리턴하자.
```python
from datetime import datetime, timedelta

def get_date_list(s, e, f="%Y%m%d", add_days=0):
    daydiff = (datetime.strptime(e.strftime(f), f) - datetime.strptime(s.strftime(f), f)).days
    return [(s + timedelta(days=x) + timedelta(days=add_days)).strftime(f) for x in range(0, daydiff + 1)] if e.strftime(f) >= s.strftime(f) else []
```
