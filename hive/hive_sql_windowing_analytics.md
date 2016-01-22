## Windowing and Analytics Functions
https://cwiki.apache.org/confluence/display/Hive/LanguageManual+WindowingAndAnalytics


###Windowing functions
##### LEAD, LAG
https://awhan.wordpress.com/2015/11/25/apache-hive-windowing-functions-lag-and-lead/
ROW기준으로 LAG함수는 이전 행의 값을 가져올 수 있고, LEAD는 다음행의 값을 가져올 수 있다.

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
##### ROW_NUMBER
##### RANK, DENSE_RANK
순위를 매길때 RANK는 등수에 2명이상 존재하면, 다음 등수에 중복되는 수를 건너뛴 등수를 넣는다. 
예를들어 2등이 2명이면 3등없이, 바로 4등이 된다.
http://thehobt.blogspot.kr/2009/02/rownumber-rank-and-denserank.html
##### CUME_DIST
##### PERCENT_RANK
##### NTILE


### Examples

### 기타 정리
##### rank() over partition by 구문과 grouping set과 함께 사용도 가능하다.
```
~
```
