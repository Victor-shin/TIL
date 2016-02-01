## linux에서 간단한 서비스(service)를 등록해보자. 

- 출처 : http://roughexistence.tistory.com/125

- tomcat의 예
```
#!/bin/sh

# Startup scipt for Tomcat
#
# chkconfig: 35 85 15
# description: apache tomcat 5.x
#
# processname: tomcat

#deamon이란 명령어는 functions라는 스크립트에서 인클루드 된 것이고,
# Source funtion library
. /etc/rc.d/init.d/functions

# 환경변수를 사용하기 위해 .bash_profile을 초기화 해줬다.
# 환경변수에서 $CATALINA_HOME, $JAVA_HOME은 필수로 export 되어 있어야 한다.
CATALINA_HOME=<톰켓 설치경로>
JAVA_HOME=<자바 설치경로>
 
export CATALINA_HOME
export JAVA_HOME

# See how we were called
case "$1" in
    start)
        echo -n "Starting tomcat: "
        daemon $CATALINA_HOME/bin/startup.sh
        touch /var/lock/subsys/tomcat
        echo
        ;;

    stop)
        echo -n "Shutting down tomcat: "
        daemon $CATALINA_HOME/bin/shutdown.sh
        touch /var/lock/subsys/tomcat
        echo
        ;;

    restart)
        $0 stop
        sleep 5
        $0 start
        ;;

    *)
        echo  "Usage: $0 {start|stop|restart}"
        exit 1
esac
exit 0
```

## etc
##### nohup
```
- nohup?
hang-up signal이 와도 동작하기 때문에 터미널 연결이 끊어져도 실행을 멈추지 않습니다.
```

service등록해서 서비스 하기전에 테스트 용도로만 프로세스를 띄워서 실행하기 위한 방법으로
nohup을 사용해서 띄울 수 있다.

예전에는 백그라운드로 실행 시키면 터미널 연결이 끊어져도 백그라운드로 실행이 되었으나 최근에는 그렇지 않은 경우도 있다.
확인 방법은 다음과 같다.
```
[ testserver ~]$ shopt | grep huponexit
huponexit      	off
```

##### node
- pm2
- foreverjs
