## input type="checkbox" 일 경우, ng-true-value가 dynamic하게 값 변경이 안되는 경우
http://stackoverflow.com/questions/24758681/angularjs-checkbox-dynamic-ng-true-value-expression
```
Expression in the ng-true-value will be evaluated only once, so it won't be dynamic.

```
결론은 ng-true-value는 오직 한번만 값이 evaluated 되기 때문에 dynamic하게 할 수 없다.
실제로 해보니 값 변경이 안된다. (왜 안되나 함참 확인하였다..)

그래서 그냥 별도로 체크값과 상태값을 분리하였다. 
체크값 : req.query_type_checker
상태값 : req.query_type 
상태값은 ng-change 이벤트 발생시 fetchqueryTypes()에서 req.query_type값을 변경하도록 하였다.
```
...(중략)...
    <label>
        <input type="checkbox" ng-model="req.query_type_checker" ng-change="fetchQueryTypes(req.ioflag);">{{query_type_names}}
    </label>
...(중략)...

```

