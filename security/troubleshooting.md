## SSH : ansible에서 publickey 에러 발생 
##### 오류 메세지 
```
...(중략)...
failed: [web] => {"cmd": "/usr/bin/git ls-remote origin -h refs/heads/web-tool-prototype", "failed": true, "rc": 128}
stderr: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.

msg: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
...(중략)...
```

##### 결론 
결론은 위의 케이스는 ansible에서 각 호스트별로 지정된 private key와 github에 등록되어 있는 public key가 맞지 않아서 였다.
private key와 public key를 새로 만들어서 처리하였다.

##### 해결방법
다음 구문으로 실제로 사용되는 private / public key가 무엇인지 확인하면 문제를 빨리 해결 할 수 있다.
```
ssh -vT git@github.xxxxxxxx.com
```

- ssh key 생성 
https://git-scm.com/book/ko/v1/Git-%EC%84%9C%EB%B2%84-SSH-%EA%B3%B5%EA%B0%9C%ED%82%A4-%EB%A7%8C%EB%93%A4%EA%B8%B0

#### 상세설명
위의 케이스는 local 및 배포가 진행되어야 하는 remote server에서 github과 연결 테스트를 했을 때에도 이상이 없었다.
```
[deploy@sua-d-tool sua-web]$ ssh -T git@github.xxxxxxxx.com
Hi search-log/sua! You've successfully authenticated, but GitHub does not provide shell access.
[deploy@sua-d-tool sua-web]$ ssh -vT git@github.xxxxxxxx.com
...(중략)...
debug1: Server accepts key: pkalg ssh-rsa blen 535
debug1: Authentication succeeded (publickey).
...(중략)...
```
그러나 위에서 보면 선택된 키가 기존의 키(sua)가 아니라 ssh-rsa였다.
실제 연결되고 정상적인 키는 rsa키였고, ansible에서는 sua키(github에 등록되어 있지 않은)였기 때문에
local 이나 remote server에서 ssh로 테스트했을 때는 정상적으로 연결되는 걸로 보이나, ansible로 배포시에는 오류가 발생하였다.
