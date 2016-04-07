## (Cloudera) Hive on Spark
http://www.cloudera.com/documentation/enterprise/5-5-x/topics/admin_hos_oview.html

http://www.cloudera.com/documentation/enterprise/latest/topics/admin_hos_config.html

(cloudera) hive on spark 
http://www.cloudera.com/documentation/enterprise/latest/topics/admin_hos_config.html#concept_mb4_g2w_3r__section_hd1_nyv_yr

```
set hive.execution.engine=spark;

select *
  from test
 where 1 = 1
   and dt = '20160405' 
   and hh = '15'
   ;
```

- Job Browser와 연동은 잘 안되는 걸로 확인된다.
- 샘플 SQL의 수행속도는 mr engine로 수행시보다 2배 빠른걸로 확인된다.
  - mr engine = 41~46 초
  - spark engine = 19 초
  
