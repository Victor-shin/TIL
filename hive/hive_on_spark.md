## (Cloudera) Hive on Spark
### 결론
#### 5.7 버전에서는 쓸만한 것 같다. 조사중
http://www.cloudera.com/documentation/enterprise/latest/topics/admin_hos_oview.html

#### 현재 5.5.x 버전인데, 서비스 버전으로는 쓰지 않도록 권장하고 있다.
### 상세 테스트
#### 환경설정
(cloudera) hive on spark 
http://www.cloudera.com/documentation/enterprise/latest/topics/admin_hos_config.html#concept_mb4_g2w_3r__section_hd1_nyv_yr

#### HUE에서 테스트
```
set hive.execution.engine=spark;

select *
  from test
 where 1 = 1
   and dt = '20160405' 
   and hh = '15'
   ;
```

- Hue와 Job Browser가 연동이 잘 안되는걸 확인했다.
  - Job Browser에서는 수행중인 작업으로 보이나(never ending), 실제로 Hue를 refresh해보면 결과가 나온다.
- 샘플 SQL의 수행속도는 mr engine로 수행시보다 2배 빠른걸로 확인된다.
  - mr engine = 41~46 초
  - spark engine = 19 초
  

#### Beeline에서 테스트
```
beeline -u jdbc:hive2://test:10000/default
set hive.execution.engine=spark;

select count(*)
  from test
 where 1 = 1
   and dt = '20160405' 
   and hh = '15'
   ;
```
- 동일한 쿼리 수행 결과 잘 돌아간다.
- 쿼리 수행 시간은 17초. 총 수행시간은 39초가 소요되었다.

###  비교
#### VS mr engine
```
set hive.execution.engine=mr;
```
쿼리 수행 시간은 31초, 총 수행시간은 47초가 소요되었다.

#### VS spark scala
```
scala> val logFiles = "/test/201604/05/15/*.gz"
logFiles: String = /test/201604/05/15/*.gz
scala> val cnt = sc.textFile(logFiles).count()
16/04/07 17:39:27 INFO MemoryStore: ensureFreeSpace(196696) called with curMem=449370, maxMem=556038881

16/04/07 17:39:40 INFO DAGScheduler: Job 2 finished: count at <console>:23, took 13.349757 s
cnt: Long = 2243815
```
총 수행시간 13초
