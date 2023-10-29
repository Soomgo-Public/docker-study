# Update the application

소스코드를 업데이트 하고 새롭게 도커를 시작하려면 아래의 프로세스를 거쳐야 한다.

1. 기존 Docker 컨테이너 삭제
2. 새롭게 이미지 빌드
3. 컨테이너로 빌드된 이미지 실행

<br/>

도커의 컨테이너를 삭제하려면 컨테이너를 우선적으로 멈추어야 한다.<br/>

즉, 아래의 플로우를 따르게 된다.

```
1. docker stop container
2. docker rm container
```

하지만 `docker rm -f container`명령어를 통해 한번에 삭제할 수 있다

> git 때문인지 포스에 대한 거부 반응이..
