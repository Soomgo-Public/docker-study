# Containerize an application

어플리케이션을 컨테이너화 하는 것은 크게 두 가지 프로세스를 거친다.<br/>

1. 이미지를 빌드하고,
2. 빌드된 이미지를 컨테이너로 실행한다.

## 이미지 빌드

- Dockerfile을 통해 이미지를 생성한다.
  - 루트 디렉토리를 따라간다.
- `docker build`명령어를 통해 이미지를 빌드한다.
  - `-t`명령어를 통해 빌드된 이미지에 유니크한 태그 값을 부여할 수 있다. (alias)

## 컨테이너 실행

- `-p`명령어를 통해 호스트의 주소와 컨테이너의 포트를 맵핑할 수 있다.<br/>
  `HOST`:`CONTAINER`<br/>예를들어<br/>
  `docker run -p 127.0.0.1:3000:3000`
  위의 명령어는 컨테이너의 3000포트를 호스트의 127.0.0.1:3000에 맵핑하게 된다.
  - `-d`명령어를 통해 백그라운드에서 컨테이너를 실행할 수 있다.

<br/>

- `ps` 명령어를 통해 실행중인 컨테이너 목록을 확인할 수 있다.
- `-it`컨테이너에 tty를 할당하고 컨테이너 내부 프롬프트로 접근할 수 있다.

<br/>

# Genie's Action Items

## NAT, NAPT와 포트 포워딩

**_Genie의 궁금점_**<br/>

> 세 개가 대체 뭔차이 ...? 같은 말?

### NAT (Network Address Translation)

로컬 IP를 공인 IP로 바꿔주는 것을 지칭.

- 로컬 장치가 공인 IP 주소와 통신할 때 사용.

### NAPT (Network Address and Port Translation)

NAT의 일종으로 IP 주소 및 포트 변환을 수행.

### 포트포워딩

NAT의 일종으로 공인 IP 주소를 통해 특정 로컬 장치로 트래픽을 라우팅하는 메커니즘.

**_결론은_** <br/>

- NAT은 `기술 또는 메커니즘 자체`를 가리킨다.
- NAPT는 NAT의 한 형태로 트래픽을 관리하는 `방법`을 의미한다.<br/>
- 포트 포워딩은 NAT 또는 NAPT의 일종으로 `라우팅하는 방법`(메커니즘)을 가리킨다.

<br/>

## DHCP (Dynamic Host Configuration Protocol)

네트워크에서 IP 주소와 관련된 다양한 네트워크 구성 정보를 동적으로 할당하고 관리하기 위한 프로토콜.
장치가 네트워크에 연결될 때

- IP 주소
- 서브넷 마스크
- 기본 게이트웨이
- DNS 서버 주소 및 기타 네트워크 설정과 같은 구성 정보를 자동으로 획득하게 한다.

<br/>

<a href="https://github.com/wonjin-dev/wikis/blob/main/CS/03.%20DHCP.md">DHCP 좀 더 알아보기</a>
