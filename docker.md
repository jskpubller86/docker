# Docker 란?

Docker는 2013년 3월 Docker, Inc(구 dotCloud)에서 출시한 오픈 소스 컨테이너 프로젝트입니다.

하나의 하드웨어에서 여러 사용자가 개별 서비스를 이용하기 위해서 가상화 라는 기술이 나왔다. 하지만 가상화라는 기술에는 다음과 같은 단점이 있었다. 

사용자가 만약 3개의 서비스를 사용하고 싶다면 가상화를 3개 만들어 사용해야 하며 3개의 가상화에는 각각 os가 설치된다. 이 os는 중복되는 운영체제로 실제로 사용자가 사용하는  서비스에 사용하지 않는 공간이 많이 생기게 되어 과금이 발생한다. 

또한 이용하던 서비스를 다른 공간으로 옮기려 한다면 작업 시간이 많이 들것이다. 그래서 리눅스에서는 이러한 중복되는 os와 서비스를 손쉽게 설치하고 해제 할 수 있도록 docker라는 기술을 제공하고 있다. 

이러한 페러다임을 Immutable Infrastructure라 말하며  운영체제는 변하지 않고 (Immutable: 불변) 서비스만 변하는 것은 말하는 것이다. 

docker는 서비스의 환경을 하나의 이미지로 만들어 docker 허브라는 공간에서 올릴 수도 있으며 다른 사용자가 만든 서비스 환경 이미지를 가져와 설치할 수도 있다.

※ 리눅스에는  컨테이너 기술이 있기 때문에 손쉽게 docker를 구현할 수 있다.

※ docker는 호스트의 자원을 사용하므로 관리자 권한으로 명령어를 실행해야 한다.

# 도커 환경 구축하기

먼저 도커를 리눅스에 설치해야 한다.  도커를 다운받기 위해서 패키지 매니저인 apt에서 관리하는 sources.list

docker의 저장소를 추가해야 한다. 

~~~
# gedit /etc/apt/sources.list    →  gedit로 sources.list 파일을 연다. 그리고 아래의 소스를 마지막에 추가한다.
​~~~~~~~~~~~~~~~~~~~
deb https://apt.dockerproject.org/repo ubuntu-xenial main
~~~

docker 패키지 저장소 주소는 https로 통신하기 때문에 https 통신을 지원하는 패키지와 공개키를 설치해야한다.

먼저 https 패키지를 설치한다. 

~~~
# apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
~~~

공개키를 다운받는다.

~~~
# apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
~~~

apt 패키지를 목록을 업데이트 해준다. 

~~~
# apt-get update
~~~

이미지를 만들려면 이미지를 만들려면 linux-image-extra 패키지가 필요하다. apt-get으로 설치해준다.

~~~
# apt-get install linux-image-extra-$(uname -r)  →  $(usernam -r) 리눅스의 버전 정보를 가져온다.
~~~

docker-engine 패키지를 설치한다.

~~~
# apt-get install docker-engine
~~~

 잘 설치가 되었는지 docker의 version을 확인한다.

~~~
# docker version
~~~

설치가 잘되었다면 도커를 실행해 준다. 

~~~
service docker start
~~~



# docker hub에서 이미지 검색

도커 허브 도커 이미지를 공유하는 원격 저장소이다.  아래와 같이 명령어를 입력한다.

~~~
# docker search <이미지 이름> → 찾고자 하는 이미지를 검색한다.
~~~



# 실행 중인 컨테이너 멈추기 

실행 중인 컨테이너를 멈추기 위해서는 





# 컨테이너 

- 특정 이름의 컨테이너를 조회

  ~~~
  # docker container ls -a --filter="name=000"   →  --filter 옵션은 이름을 필터한다.
  ~~~

- 특정 이름의 컨테이너를 삭제

  ~~~
  # docker container rm -f $(docker container ls -aq --filter="name=ooo")
  ~~~

- 특정 이름의 컨테이너를 삭제하고 해당 이름의 컨테이너를 실행

  ~~~
  docker container rm -f $(docker container ls -aq --filter="name=ooo") ; docker container run --name ooo IMAGE_NAME   → --name 옵션은 컨테이너 이름을 지정한다.
  ~~~





# 포트포워딩



# docker-compose를 이용한 docker 이미지 조작

docker-compose는 yaml을 사용한다. 

