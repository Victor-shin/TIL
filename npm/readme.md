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
