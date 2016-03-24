## ng-true-value는 dynamic하게 값 변경이 안된다.
http://stackoverflow.com/questions/24758681/angularjs-checkbox-dynamic-ng-true-value-expression
```
Expression in the ng-true-value will be evaluated only once, so it won't be dynamic.

```
- 결론: ng-true-value는 오직 한번만 값이 evaluated 되기 때문에 dynamic하게 할 수 없다.
- 해결: 체크 변수와 상태값 저장변수를 분리하였다. 
  - 체크값 : req.query_type_checker
  - 상태값 : req.query_type 
  - 상태값은 ng-change 이벤트 발생시 fetchqueryTypes()에서 req.query_type값을 변경하도록 하였다.
```
...(중략)...
    <label>
        <input type="checkbox" ng-model="req.query_type_checker" ng-change="fetchQueryTypes(req.ioflag);">{{query_type_names}}
    </label>
...(중략)...
```

```
...(중략)...
if($scope.req.query_type_checker) {
    $scope.req.query_type = queryType;  
} else {
    $scope.req.query_type = [];
}
...(중략)...
```
