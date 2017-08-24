## Vectorized Query Execution
https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution

##### vectorized execution
tinyint
smallint
int
bigint
boolean
float
double
decimal
date
timestamp
string

##### expressions can be vectorized
- arithmetic: +, -, *, /, %
- AND, OR, NOT
- comparisons <, >, <=, >=, =, !=, BETWEEN, IN ( list-of-constants ) as filters
- Boolean-valued expressions (non-filters) using AND, OR, NOT, <, >, <=, >=, =, !=
- IS [NOT] NULL
- all math functions (SIN, LOG, etc.)
- string functions SUBSTR, CONCAT, TRIM, LTRIM, RTRIM, LOWER, UPPER, LENGTH
- type casts
- Hive user-defined functions, including standard and generic UDFs
- date functions (YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, UNIX_TIMESTAMP)
- the IF conditional expression

##### 기타의견
- 위에 언급된 표현식중에 string functions중에 CONCAT을 쓰고 쿼리 실행계획을 살펴보니, vectorized mode가 없어지는게 보여진다.
- record사이즈에 따라 다르겠지만 약 2천만건의 records를 count(*)하는 연산이 vectorized mode의 경우 18~19s소요되었고
일반 모드(concat썼을 때) 20여초가 소요되었다.
- cube 함수를 써도 vectorized mode가 안된다. analytic functions도 안되나보다.
