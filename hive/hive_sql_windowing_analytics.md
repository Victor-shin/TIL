## Windowing and Analytics Functions

https://cwiki.apache.org/confluence/display/Hive/LanguageManual+WindowingAndAnalytics

### Windowing functions

### The OVER clause
#### There can be multiple OVER clauses in a single query.
```
SELECT 
 a,
 COUNT(b) OVER (PARTITION BY c) AS b_count,
 SUM(b) OVER (PARTITION BY c) b_sum
FROM T;
```

### Analytics functions
#### RANK
#### ROW_NUMBER
#### DENSE_RANK
#### CUME_DIST
#### PERCENT_RANK
#### NTILE

## 기타 참고 링크
