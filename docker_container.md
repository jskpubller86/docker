# 도커 컨테이너 실행하기 

도커 컨테이너를 실행하려면  `run` 명령을 이용한다.

~~~  
# docker run <도커 이미지> → 도커 이미지를 foreground 로 실행한다.
# docker run -d <도커 이미지> → 도커 이미지를 background 로 실행한다.
# docker run -p 8081:8080 <도커 이미지> → 포트를 8081포트를 8080포트로 매핑해준다.
~~~

# 호스트와 도커 컨테이너 볼륨 공유

도커 컨테이너를 실행할 때 도커 컨테이너 볼륨과 호스트 볼륨을 설정할 수 있다.  볼륨을 설정할 때는 `-v` 옵션을 설정한다.  

만약 data 폴더를 공유한다면 아래와 같이 할 수 있다.

```
# docker run -i -t --name hello-volume1 -v /root/data:/data ubuntu /bin/bash
```

위에서 `/root/data:/data` 부분에서 `/root/data` 부분은 공유할 호스트 볼륨이며 뒤에 `/data`  는 컨테이너 볼륨이다.  구분은 `:`  으로 한다. 

호스트 볼륨의 경로는 반드시 절대 경로를 지정해야 한다.

# 도커 컨테이너 삭제하기 

~~~
# docker container rm <도커 이름 | 도커 아이디>
# docker rm <도커 이름 | 도커 아이디>
# docker rm <>
~~~



# 도커 컨테이너에서 명령 실행하기

도커 컨테이너에 명령을 실행할 수  있다. 명령어 기본 포맷은 아래와 같다.

```
# docker exec -it <container id | container name> <command>
```

예를 들어 아파치 서버에서 서버를 실행하는 명령어는 아래와 같다. 

```
# docker exec -it my-apache-app httpd:2.4
```

도커 컨테이너의 쉘을 실행하면  컨테이너에서 쉘 명령을 실행할 수 있다. 

```
# docker exec -it my-apache-app /bin/sh
```

도커 실행할 때  명령을 실행할 수 있다.

~~~
# docker run -it my-apache-app /bin/sh
~~~

 

