##   export
beeline을 통해서 table을 export가 동작하지 않는다.
상황은 쿼리가 복잡해서 'set'을 통해서 hive query 환경 설정을 변경하였다.
```
set hive.new.job.grouping.set.cardinality=128;
```
그 이후에 다시 cardinality값을 30 (default) 값으로 변경 한후에 table export하니 안되더라.

그래서 cardinality값을 30으로 원복하기 전에 export 하니까 되더라 
