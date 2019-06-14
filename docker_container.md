# 도커 컨테이너 실행하기 

도커 컨테이너를 실행하려면  `run` 명령을 이용한다.

~~~  
# docker run <도커 이미지> → 도커 이미지를 foreground 로 실행한다.
# docker run -d <도커 이미지> → 도커 이미지를 background 로 실행한다.
# docker run -p 8081:8080 <도커 이미지> → 포트를 8081포트를 8080포트로 매핑해준다.
~~~

# 호스트와 도커 컨테이너 볼륨 공유

볼륨 공유 방식은 크게 세가지다. 

- bind mount - 바인딩 방식 
- volume - 도커볼륨 공유 방식
- tmpfs mount  - 메모리 공유방식

### bind mount - 바인딩 방식

도커 컨테이너를 실행할 때 도커 컨테이너 볼륨과 호스트 볼륨 bind mount 할 수 있다.  볼륨을 설정할 때는 `-v` 옵션을 설정한다.  

bind mount 방식은 호스트 볼륨이 우선이기 때문에  마운트 하려는 컨테이너 볼륨에 파일이 있다면 마운트 되는 순간 호스트 볼륨의 파일만 보여지고 기존에 있던 컨테이너 볼륨의 파일은 숨겨지게된다.

```예시 코드
# docker run -i -t --name hello-volume1 -v /root/data:/data ubuntu /bin/bash
```

위에서 `/root/data:/data` 부분에서 `/root/data` 부분은 공유할 호스트 볼륨이며 뒤에 `/data`  는 컨테이너 볼륨이다.  구분은 `:`  으로 한다. 

호스트 볼륨의 경로는 반드시 절대 경로를 지정해야 한다.

### volume - 도커 볼륨 방식

도커 볼륨 방식은 도커에서 관리할 수 있는 볼륨을 생성하고 그 볼륨을 컨테이너와 공유하는 방식이다. 

`docker volume` 명령으로  쉽게 관리 할 수 있다. 

`bind mount`  방식과 차이는 마운트 하기보다는  공유를 하여  호스트 볼륨의 파일과 컨테이너 볼륨의 파일을 모두 확인 할 수 있다는 것이다.



도커의 볼륨을 생성한다.

~~~~ 
# docker volume create myvolume  → myvolume으로 도커 볼륨을 생성한다.
# docker volume <ls | list> → 생성된 도커 볼륨들을 확인한다.
~~~~

생성된 도커 볼륨과 컨테이너의 볼륨을 연결하려면 아래와 같이 한다. 

~~~
# docker run -i -t --name hello-volume1 -v myvolume:/myvolume ubuntu /bin/bash
~~~

모든 도커 볼륨 삭제 

~~~ 
# docker volume prune
~~~

### tmfs mount



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

#  컨테이너 접속하기

attach 명령을 이용하면  쉽게 접속할 수 있습니다.

~~~~
# docker attach <컨테이너 id | 컨테이너 이름 >
~~~~



