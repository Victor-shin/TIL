# 7장 특수 RDD 연산

7장에서 다루는 내용

* RDD타입
* 집계
* 파티셔닝 및 셔플링
* 브로드캐스트 변수
* 누산기

## RDD 타입

### 쌍 RDD
쌍(pair) RDD는 집계, 정렬, 데이터 조인과 같은 많은 사용 사례에 적합한(키-값) 튜플로 구성된 RDD다.

### DoubleRDD
double 값의 모음으로 구성된 RDD다.

### SequenceFileRDD
SequenceFileRDD는 하둡 파일 시스템의 파일 포멧인 SequenceFile에서 생성된다.
SequenceFile은 압축될 수 있고, 압축이 해제될 수 있다.

### CoGroupRDD
RDD의 부모와 함께 그룹핑되는 RDD다.

### ShuffledRDD
키별로 RDD 엘리먼트를 섞어 동일한 익스큐터에서 동일한 키에 대한 값을 누적해 집계하거나 로직을 결합할 수 있다.

### UnionRDD
두 개의 RDD에 유니온(union) 연산을 적용한 결과다.
(실습결과) SQL의 union all과 같은 효과로 확인되었다

### HadoopRDD
하둡 1.x 라이브러리의 맵 리듀스 API를 사용해 HDFS에 저장된 데이터를 읽는 핵심 기능을 제공한다.
HadoopRDD는 기본적으로 사용되며, 모든 파일 시스템의 데이터를 RDD로 로드할 때 HadoopRDD를 볼 수 있다.

### NewHadoopRDD
하둡 2.x 라이브러리의 새로운 맵 리듀스 API를 사용해 HDFS, HBase 테이블, 아마존 S3에 저장된 데이터를 읽는 핵심 기능을 제공한다. 
NewHadoopRDD는 다양한 포멧으로 읽을 수 있기 때문에 여러 외부 시스템과 상호작용 하기 위해 사용된다. 


## 집계

### groupByKey
결과 RDD는 계산될 때마다 다를 수 있다.
많은 셔플링을 포함한다.

### reduceByKey
로컬 컴바이너(combiner)를 사용해 먼저 로컬에서 일부 기본 집계를 수행한 다음 groupByKey처럼 결과 엘리먼트를 전송시켜 성능을 향상시킨다.

### aggregateByKey
* reduceByKey와 매우 유사하다.
* aggregateByKey를 사용하면 파티션 집계가 유연하고 사용자 정의가 가능하다.

### combineByKey

### groupByKey, reduceByKey, combineByKey, aggregateByKey의 비교


## 파티셔닝과 셔플링
RDD는 클러스터 전체에 분산된 파티션 데이터를 관리한다.

### 파티셔너
파티셔너(Partitioner)에 의해 RDD 파티셔닝이 실행된다.

* HashPartitioner
* RangePartitioner

### 셔플링
* 파티셔너가 어떤 파티션을 사용하든 많은 연산이 RDD의 파티션 전체에 걸쳐 데이터 리파티셔닝(repartitioning)이 발생하게 된다.
* 리파티셔닝에 필요한 모든 데이터 이동을 셔플링(shuffling)이라 한다.

* 의존성
  * 좁은 의존성(narrow dependency)
  * 넓은 의존성(wide dependency)

## 브로드캐스트 변수
* 브로드캐스트 변수는 모든 익스큐터에서 사용할 수 있는 공유 변수(shared variable)다.
* 드라이버에서 한 번 생성되면 익스큐터에서만 읽을 수 있다.


### 브로드캐스트 변수 생성
val bc = sc.broadcast(m)

### 브로드캐스트 변수 정리
val bk = sc.broadcast(k)
bk.unpersist


### 브로드캐스트 정리
bk.destroy


## 누산기
스파크 프로그램에 카운터를 추가하기 위해 일반적으로 사용되는 익스큐터에서 변수를 공유한다.


## 요약



