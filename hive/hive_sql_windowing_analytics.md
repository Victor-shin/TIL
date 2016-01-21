## Windowing and Analytics Functions
https://cwiki.apache.org/confluence/display/Hive/LanguageManual+WindowingAndAnalytics


###Windowing functions
##### LEAD
##### LAG
##### FIRST_VALUE
##### LAST_VALUE

### The OVER clause
다음의 형식으로 사용할 수 있다.
```
OVER ~ PARTITION BY ~ ORDER BY
```

두개 OVER ~ PARTITION 구분이 사용될 수도 있다.
```
SELECT a,
       COUNT(b) OVER (PARTITION BY c) AS b_count,
       SUM(b) OVER (PARTITION BY c) b_sum
  FROM T;
```

OVER와 window 명세. Windows는 WINDOW 문구로 분리해서 사용될 수 있다.
```
SELECT a, SUM(b) OVER w
FROM T;
WINDOW w AS (PARTITION BY c ORDER BY d ROWS UNBOUNDED PRECEDING)
```

### Analytics functions
##### RANK
##### ROW_NUMBER
##### DENSE_RANK
##### CUME_DIST
##### PERCENT_RANK
##### NTILE


### Examples

### 기타 정리
##### rank() over partition by 구문과 grouping set과 함께 사용도 가능하다.
```
~
```
