# 도커 이미지 만드는 방법 

도커 이미지 파일을 만드는 방법은 크게 세가지다. 

- Dockerfile을 이용한 방법
- 

도커의 이미지를 만들 때는 [ docker image  build ] 명령을 사용한다.

```
# docker image build -t path/name:latest
```

- -t 옵션은 이미지에 태그를 작성할 수 있게 하는 옵션이다.  
- path/name:latest 
  - path는 이미지 파일 이름을 구별해주기 위한 패스네임을 적용해준다. 도커 허브에서 구별될 수 있도록 작성해줘야 한다. 보통 도커허브의 아이디를 입력한다.
  - name은 이미지 이름을 작성해 준다. 
  - :latest 는 태그입력 부분으로 보통 이미지의 버전 작성하여 관리한다.

도커가 도커 이미지를 생성하면 image id가 생성된다.

도커 이미지를 생성하였다면 아래의 명령들로 만든 이미지를 확인할 수 있다.

```
# docker image ls    → 도커 이미지를 보여준다.
# docker images	     → 도커 이미지를 보여준다.
```

<table>
    <tr>
    	<th>REPOSITORY</th>
        <th>TAG</th>
        <th>IMAGE ID</th>
        <th>CREATED</th>
        <th>SIZE</th>
    </tr>
    <tr>
    	<td>path/name</td>
        <td>latest</td>
        <td>6775e8903765</td>
        <td>4 minutes ago</td>
        <td>750MB</td>
    </tr>
</table>

그럼 도커 이미지를 만드는 상황을 보자 

간단하게 golang을 이용하여 웹서버를 실행하는  명령을 만들어 보자.

우선 docker 라는 디렉터리를 만들고 해당 폴더로 이동한다.

```
# mkdir docker
# cd docker
```

이제 golang 언어를 이용한  웹서버 프로그램을 만들어 보자

```
# gedit main.go
```

main.go

```main.go
package main

import ( 
	"fmt" 
	"log"
	"net/http"
)

func main() {
    	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		log.Println("received request")
		fmt.Fprintf(w, "Hello Docker !!!")
    	})
	log.Println("start server")

	server := &http.Server{Addr: ":8080"}
	if err := server.ListenAndServe(); err != nil {
		log.Println(err)
	}
}
```

이제 main.go 파일을 도커 이미지 파일로 만들어보자 

```
# docker image build -t example/echo:latest .	→  
# docker iamges 
```

# 도커 이미지 검색

호스트에 있는 도커 이미지는 `docker images` 명령을 통해서 확인할 수 있다. 

~~~ 간단하게 표현한 docker images
# docker image ls       → 도커 이미지를 보여준다.
# docker images	        → 도커 이미지를 보여준다.
# docker images ubuntu  → 도커 이미지 이름이 ubuntu 인 것을 보여준다.

~~~

~~~docker images manual
NAME
       docker-images - List images

SYNOPSIS
       docker images [OPTIONS] [REPOSITORY[:TAG]]

DESCRIPTION
       Alias for docker image ls.

OPTIONS
       -a, --all[=false]
           Show all images (default hides intermediate images)

       --digests[=false]
           Show digests

       -f, --filter=
           Filter output based on conditions provided

       --format=""
           Pretty-print images using a Go template

       --no-trunc[=false]
           Don't truncate output

       -q, --quiet[=false]
           Only show numeric IDs

~~~

# 도커 허브에서 이미지 검색

도커 허브의 이미지를 검색할 때는 `docker search` 를 이용한다. 아래는 해당 메뉴얼이다.

~~~
NAME
       docker-search - Search the Docker Hub for images

SYNOPSIS
       docker search [OPTIONS] TERM

DESCRIPTION
       Search Docker Hub for images that match the specified TERM. The table of
       images returned displays the name, description (truncated by default),
       number of stars awarded, whether the image is official, and whether it is
       automated.

       Note - Search queries will only return up to 25 results

Filter
       Filter output based on these conditions:
          - stars=<numberOfStar>
          - is-automated=(true|false)
          - is-official=(true|false)

EXAMPLES
Search Docker Hub for ranked images
       Search a registry for the term 'fedora' and only display those images ranked
       3 or higher:

              $ docker search --filter=stars=3 fedora
              NAME                  DESCRIPTION                                    STARS OFFICIAL  AUTOMATED
              mattdm/fedora         A basic Fedora image corresponding roughly...  50
              fedora                (Semi) Official Fedora base image.             38
              mattdm/fedora-small   A small Fedora image on which to build. Co...  8
              goldmann/wildfly      A WildFly application server running on a ...  3               [OK]

Search Docker Hub for automated images
       Search Docker Hub for the term 'fedora' and only display automated images
       ranked 1 or higher:

              $ docker search --filter=is-automated=true --filter=stars=1 fedora
              NAME               DESCRIPTION                                     STARS OFFICIAL  AUTOMATED
              goldmann/wildfly   A WildFly application server running on a ...   3               [OK]
              tutum/fedora-20    Fedora 20 image with SSH access. For the r...   1               [OK]

OPTIONS
       -f, --filter=
           Filter output based on conditions provided

       --limit=25
           Max number of search results

       --no-trunc[=false]
           Don't truncate output

~~~

# 도커 허브에서 이미지 받기 

도커 허브에서 이미지를 받을 때는 pull 명령을 사용합니다. 

`docker pull <이미지 이름>:<태그>` 형식입니다. latest를 설정하면 최신 버전을 받습니다. **ubuntu:14.04**, **ubuntu:12.10**처럼 태그를 지정해 줄 수도 있습니다.

~~~
# docker pull ubuntu:latest
~~~

이미지 이름에서 **pyrasis/ubuntu**처럼 / 앞에 사용자명을 지정하면 Docker Hub에서 해당 사용자가 올린 이미지를 받습니다. 공식 이미지는 사용자명이 붙지 않습니다.

~~~
# docker pull pyrasis/ubuntu:latest
~~~

# 도커 이미지 삭제

호스트에 있는 도커 이미지를 삭제하려면 아래와 같이 한다. 

~~~ 
# docker rmi <도커 이름>         
# docker rmi <도커 이미지 id>  
# docker rmi $(docker images -q) →  호스트에 있는 도커 이미지들을 삭제 한다. 
~~~

아래는 `docker rmi` 의 메뉴얼이다.

~~~
NAME
       docker-rmi - Remove one or more images

SYNOPSIS
       docker rmi [OPTIONS] IMAGE [IMAGE...]

DESCRIPTION
       Alias for docker image rm.

OPTIONS
       -f, --force[=false]
           Force removal of the image

       --no-prune[=false]
           Do not delete untagged parents
~~~

