## linux tomcat을 service로 등록해보자. 

- 출처 : http://roughexistence.tistory.com/125

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
