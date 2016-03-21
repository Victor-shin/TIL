## 개발/라이브 환경 설정
#####출처 
http://inspiredjw.tistory.com/entry/Nodejs-%EC%97%90%EC%84%9C-NODEENV-%EA%B0%92%EC%9C%BC%EB%A1%9C-%ED%99%98%EA%B2%BD-%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0

##### 요약
- 코드
```
process.env.NODE_ENV = ( process.env.NODE_ENV && ( process.env.NODE_ENV ).trim().toLowerCase() == 'production' ) ? 'production' : 'development';
var JENKINS_SERVER_URL = '테스트 JENKINS SERVER URL';
if( process.env.NODE_ENV == 'production' ) {
    console.log("Production Mode");
    JENKINS_SERVER_URL = '서비스 JENKINS SERVER URL';
} else {
    console.log("Development Mode");
}
var jenkinsapi = require('jenkins-api');
var jenkins = jenkinsapi.init(JENKINS_SERVER_URL);
```
- 라이브 구동시
```
export NODE_ENV=production
npm start
```
