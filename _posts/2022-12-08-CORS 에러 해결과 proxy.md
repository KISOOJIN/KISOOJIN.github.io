---
title: "CORS 에러 해결과 proxy"

categories: [TIL]
comments: true

toc: true
toc_sticky: true

date: 2022-12-08
---

<h1>CORS에러 해결</h1>

![스크린샷 2022-12-08 16-43-56](https://user-images.githubusercontent.com/111376707/206390640-f61b0a46-028e-4ecf-a6d4-c945677704d3.png)

1. pre-flight로 OPTIONS 메서드를 통해 백엔드에 접근권한을 요청하여 서버측에서 CORS 설정해주면 그것을 근거로 접근할 수 있게됩니다. (정석)

2. proxy를 이용하여 우회하는 방법

- React 앱에서 브라우저를 통해 API를 요청
- proxy를 통해 백엔드 서버로 우회 요청
- 백엔드 서버에서 proxy를 통해 React 앱으로 우회하여 응답
- React 앱은 받은 응답을 백엔드 서버 대신 브라우저에게 전달(CORS ERROR X)

이렇게 되면 출처가 같아지기 때문에 브라우저는 이 사실을 눈치 채지 못하고 허용하게 됩니다.

<h1>Proxy 사용법</h1>

<h2>방법1 : webpack dev server proxy</h2>

원래 웹팩 설정을 통해서 적용하지만
CRA로 만든 React 프로젝트 에서는 package.json 에서 proxy 값을 설정하여 적용

```

< 클라이언트의 package.json >

...

"browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
	"proxy" : "우회할 API 주소"
}


```

(중요) 추가 확인 및 에러 해결사항!

![스크린샷 2022-12-08 16-42-58](https://user-images.githubusercontent.com/111376707/206396514-ac24b04d-ce0b-4d34-910b-71d1335f5904.png)

package.json 에 proxy 부분 작성 후, npm install 을 다시 해줘야 module에 반영!

그 다음은 기존의 fetch, 혹은 axios를 통해 요청하던 부분에서 도메인 부분을 제거

```javascript

// 적용 전
export async function getAllfetch() {

    const response = await fetch('우회할 api주소/params');
    .then(() => {
			...
		})
}

// 적용 후
export async function getAllfetch() {

    const response = await fetch('/params');
    .then(() => {
			...
		})
}
```

<h2>방법2 : React Proxy</h2>

webpack dev server 에서 제공하는 proxy는 전역적인 설정이기 때문에, 종종 해당 방법이 충분히 적용되지 않는 경우가 생기기도 합니다.
그래서 수동으로 proxy를 적용해줘야 하는 경우가 있는데, 이때는 <strong>http-proxy-middleware</strong> 라이브러리를 사용해야 합니다.

<br/>

http-proxy-middleware 라이브러리 설치

> npm install http-proxy-middleware --save

React App의 src 파일 안에서 setupProxy.js 파일을 생성하고, 안에서 설치한 라이브러리 파일을 불러온 다음, 아래와 같이 작성을 합니다.

```

const { createProxyMiddleware } = require('http-proxy-middleware');

module.exports = function(app) {
  app.use(
    '/api', //proxy가 필요한 path prameter를 입력합니다.
    createProxyMiddleware({
      target: 'http://localhost:5000', //타겟이 되는 api url를 입력합니다.
      changeOrigin: true, //대상 서버 구성에 따라 호스트 헤더가 변경되도록 설정하는 부분입니다.
    })
  );
};
```

그 다음은 기존의 fetch, 혹은 axios를 통해 요청하던 부분에서 도메인 부분을 제거

```javascript

// 적용 전
export async function getAllfetch() {

    const response = await fetch('우회할 api주소/params');
    .then(() => {
			...
		})
}

// 적용 후
export async function getAllfetch() {

    const response = await fetch('/params');
    .then(() => {
			...
		})
}
```
