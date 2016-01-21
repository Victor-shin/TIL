## Enhanced Aggregation, Cube, Grouping and Rollup

https://cwiki.apache.org/confluence/display/Hive/Enhanced+Aggregation,+Cube,+Grouping+and+Rollup#EnhancedAggregation,Cube,GroupingandRollup-CubesandRollups

### GROUPING SETS
GROUPING SETS은 GROUP BY가 되는 단위를 그룹단위로 지정해서 그룹핑할 수 있게 한다.

#### 일반적으로 사용되는 GROUP BY 예시
```
SELECT a, b, SUM( c ) FROM tab1 GROUP BY a, b
UNION
SELECT a, null, SUM( c ) FROM tab1 GROUP BY a

```

#### 위와 동일한 효과를 가지게 되는 GROUPING SETS 예시
```
SELECT a, b, SUM( c ) FROM tab1 GROUP BY a, b GROUPING SETS ( (a,b), a)
```

### Grouping__ID function
GROUPING SETS 문으로 인해서 NULL값이 들어가야 하는 필드에 이미 NULL 값을 가지고 있었다면, 의도한 대로 동작하지 않을 것이다.
이때 GROUPING__ID 필드를 통해 구분할 수 있다.

예시
```
SELECT key, value, GROUPING__ID, count(*) from T1 GROUP BY key, value WITH ROLLUP
```

### Cubes and Rollups
CUBE/ROLLUP은 오직 GROUP BY와 함께만 쓰일 수 있다.
CUBE는 모든 가능한 조합의 셋을 만든다.
다음의 두 GROUP BY 절은 동일하다.
```
GROUP BY a, b, c WITH CUBE 
```

```
GROUP BY a, b, c GROUPING SETS ( (a, b, c), (a, b), (b, c), (a, c), (a), (b), (c), ( )).
```

ROLLUP은 계층적인 조합의 셋을 만든다.
다음의 두 GROUP BY 절은 동일하다.
```
GROUP BY a, b, c, WITH ROLLUP
```

```
GROUP BY a, b, c GROUPING SETS ( (a, b, c), (a, b), (a), ( ))
```

### 주의할 점
대상 테이블의 컬럼의 cardinality가 너무 높다면 map-side aggregation 작업이 아름답게 돌아가지 않는다.

GROUPING SET의 cardinality값이 hive.new.job.grouping.set.cardinality 파라미터 값보다 크다면, 새로운 MR 작업이 original group by 가 데이터 사이즈를 줄일 거라는 예측 아래에 추가된다.

원문 
```
Whether a new map-reduce job should be launched for grouping sets/rollups/cubes.
For a query like: select a, b, c, count(1) from T group by a, b, c with rollup;
4 rows are created per row: (a, b, c), (a, b, null), (a, null, null), (null, null, null)
This can lead to explosion across map-reduce boundary if the cardinality of T is very high
and map-side aggregation does not do a very good job.
This parameter decides if hive should add an additional map-reduce job. If the grouping set
cardinality (4 in the example above), is more than this value, a new MR job is added under the
assumption that the orginal group by will reduce the data size.
```
