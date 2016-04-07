## (Cloudera) Hive on Spark
### 결론
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
- 쿼리 수행 시간은 17초. 총 수행시간은 39.61초가 소요되었다.
- (그외) hive execution engine을 mr로 했을 시, 쿼리 수행 시간은 31초, 총 수행시간은 47초가 소요되었다.
