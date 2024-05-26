# Image building best practices

## Image layering

`docker image history`명령을 통해 이미지 내의 각 레이어를 생성하는 데 사용된 명령을 볼 수 있다.

### caching

이전 학습을통해 레이어가 변경되면 모든 다운스트림 레이어도 다시 생성되어야 한다는 것을 알고있다. 따라서 캐싱을 통해 컨테이너 이미지의 빌드 시간을 줄일 수 있다.

```
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```

위의 Dockerfile를 실행시킨 후 `docker image history`를 통해 Dockerfile의 각 명령이 이미지의 새 레이어가 되는 것을 알 수 있다.<br/>
즉, 이미지를 변경할 때마다 종속성 패키지를 다시 설치해야 한다는 것을 의미한다.<br/>
<br/>

```
FROM node:18-alpine
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn install --production
COPY . .
CMD ["node", "src/index.js"]
```

위와 같이 변경하여 Dockerfile을 종속성 패키지를 먼저 설치 후 다른 항목을 복사할 수 있다.<br/>
이후 `.dockerignore`파일을 통해 이미지 관련 파일만 선택적으로 복사할 수 있다. 이를 통해 두 번째 COPY단계에서 `node_modules`를 생략할 수 있다.

<br/>

## Multi-stage builds

여러 단계를 사용하여 이미지를 생성하면 몇 가지 장점이 있다.

- 런타임 종속성과 빌드 시간 종속성의 분리
- 앱 실행시 필요한 것만 제공하여 이미지 경량화

리액트를 예를 들면,<br/>

```
FROM node:18 AS build
WORKDIR /app
COPY package* yarn.lock ./
RUN yarn install
COPY public ./public
COPY src ./src
RUN yarn run build

FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

위와 같이 Dockerfile을 작성했다고 가정하자.<br/>
React 애플리케이션을 구축할 때 JSX, SASS 스타일시트 등을 정적 HTML, JS 및 CSS로 컴파일 할 때만 노드 환경이 필요하다.<br/>
(SSR을 수행하지 않는 경우)<br/>
외에는 노드환경이 필요하지 않으므로, 컴파일 단계에서만 노드 환경을 제공하고, 생성된 정적 리소스만 nginx 컨테이너에 전달할 수 있다.
