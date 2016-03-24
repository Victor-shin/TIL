## forever-service

### trouble shooting
##### /usr/bin/env: node: No such file or directory
- problem
```
# service sua start
/usr/bin/env: node: No such file or directory
Starting sua
/usr/bin/env: node: No such file or directory
```
- solution
```
# which node
/daum/program/node/bin/node
# ln -s /daum/program/node/bin/node /usr/bin/node
```

- additional
"mean stack"의 서버 구동시 forever-service를 사용하게 될 경우 
bin/www의 정보 참조를 하지 않아서 인지 "프로세스"는 정상적으로 구동되나
웹서버 접근시(3000포트) 서버가 온 상태가 아닌 걸로 보인다.
아래 pm2로 서버 구동시처럼 뭔가 추가적인 작업이 필요해보인다.

## pm2
https://github.com/Unitech/pm2

### Run server with "mean stack"
```
# pm2 start bin/www
```
