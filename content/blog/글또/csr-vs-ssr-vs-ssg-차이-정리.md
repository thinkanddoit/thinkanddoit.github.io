---
title: CSR vs SSR vs SSG 차이 정리
date: 2023-06-18 18:06:72
category: 글또
thumbnail: { thumbnailSrc }
draft: false
---

[CSR vs SSR vs SSG](https://ajdkfl6445.gitbook.io/study/web/csr-vs-ssr-vs-ssg)

정리하기

## CSR vs SSR vs SSG

- 웹 페이지를 렌더링하는방식

### Client Side Rendering (CSR)

- 클라이언트(브라우저)에서 웹 페이지를 렌더링 하는 것.
- TTI === TTV
- 모든 로직, 데이터 가져오기, 템플릿, 라우팅은 서버가 아닌 클라이언트에서 처리

> CSR은 js번들 크기의 영향을 많이 받아서 적극적 `code splitting` 을 고려해야한다. (FCP최적화, TTI최적화)

\*FCP(First Contentful Paint) - 첫 유용한 콘텐츠

\*FP(First Paint) - 첫 픽셀

\*TTI(Time to Interactive)

\*TTV(Time to View)

**CSR 동작 방식**

1. 사용자의 웹 페이지 방문 (request)
2. 브라우저는 최소한 HTML 파일을 다운로드 (response)

   - 최소한 HTML(index.html)

     ```jsx
     <!DOCTYPE html>
     <html>
     <head>
       <!-- 페이지에 필요한 외부 스타일시트, 스크립트 등의 리소스를 로드하기 위한 태그 -->
       <link rel="stylesheet" href="styles.css">
       <script src="main.js"></script>
     </head>
     <body>
       <!-- 초기에 빈 콘텐츠를 가지고 있을 수도 있습니다. -->

       <!-- JavaScript와 데이터를 이용하여 동적으로 콘텐츠를 생성하는 영역 -->
       <script>
         // JavaScript 코드
         // 데이터 로딩 및 콘텐츠 생성 로직
       </script>
     </body>
     </html>
     ```

3. 브라우저는 `index.html`에 있는 js 번들 파일을 다운로드
4. `AJAX` 를 통해 `API` 요청을 수행해 동적 컨텐츠를 가져오고 파싱 → 최종 컨텐츠 렌더링
5. 사용자가 페이지를 이동하는 경우, 서버에 추가 `HTML` 파일 요청 없이 이미 받은 자바스크립트를 이용해 렌더링

**CSR 장점**

- 후속 페이지 로드 시간이 빠름 (이미 모든 스크립트가 사전 로드)
- 서버 부하 감소
- 서버 호출시 전체 UI 다시 로드할 필요 없음

**CSR 단점**

- 초기 페이지 로드가 `SSR` 에 비해 느림
- SEO에 친화적이지 않음 (검색 엔진 크롤러 방문시 빈 페이지)
  - 구글 크롤러는 js실행 시키긴 하지만 모든 검색엔진크롤러가 지원하지 않음
- 처음 HTML, JavaScript 파일 다운, 프레임워크 실행시점에 사용자가 빈 페이지를 봄

### Server Side Rendering (SSR)

- 서버의 `HTML` 로 렌더링하는 방식
- TTV >>> TTI
- 브라우저에서 응답 받기 전 데이터 패칭 및 템플릿 작성이 처리됨

**SSR 동작 방식**

1. 사용자의 웹 페이지 방문 (request)
2. 서버는 리소스 확인, 페이지 내 서버측 스크립트 실행 후 `HTML` 컨텐츠를 컴파일 및 준비
3. 컴파일된 `HTML`은 추가 렌더링 및 표시를 위해 클라이언트(브라우저)로 전송(response)
4. 브라우저는 `HTML`을 다운하고 사용자가 사이트를 볼 수 있게 함
5. 브라우저는 자바스크립트를 다운로드하고 실행하면서 `interactive`하게함
6. 사용자가 페이지를 이동할 때마다 위 동작 반복

**SSR 장점**

- 초기 페이지 로드시간이 빠름(`FP` 및 `FCP`가 빠르다)
- 이미 렌더링이 준비된 `HTML` 파일을 브라우저에서 로드하기 때문에 CSR에 비해 빠름
- 서버에서 페이지 로직 및 렌더링을 실행하면서 Js를 클라이언트에 보내지 않아도 됨으로 `TTI`를 빠르게 수행할 수 있다.
- `SEO`에 친화적이다.

**SSR 단점**

- 페이지 이동시마다 서버에서 페이지를 생성하는데 시간이 걸리기때문에 `TTFB`가 느리다.
  - TTFB(Time to First Byte)
  - 요청 후 첫 바이트 수신 시간
  - CSR은 최소한의 `HTML`을 받기에 `TTFP`가 상대적으로 낮음
- 서버 호스팅이 필요하다
- CSR에 비해 더 많은 개발 노력이 필요, SSR 프레임워크 사용시 추가 러닝 커브 비용 발생

### Static Site Generator(SSG)

- SSR처럼 서버로 부터 완성된 HTML을 받아옴.
- 차이는 HTML 파일의 생성시점이 빌드타임이다.
- Static이라는 용어는 HTML이 정적이라는 것이지 페이지가 정적인 것은 아님
- Next.js에서 권장하는 렌더링 방식

**SSG 동작 방식**

1. 사용자의 웹 페이지 방문 (request)
2. 엣지 캐싱(edge caching)된 HTML을 클라이언트로 반환
3. 브라우저는 HTML을 다운로드하고 최종 사용자가 사이트를 보게함

> 엣지 캐싱(edge caching)?
> 사용자에게 더 가까운 컨텐츠를 저장하기 위해 캐싱 서버를 사용하는 것
> 대표 : CDN

**SSG 장점**

- 빌드타임에 HTML 파일이 생성되기 때문에 빠른 FP,FCP,TTI를 제공
- 매 요청마다 생성하는 것이 아니므로, SSR과 달리 일관성 있게 빠른 TFB달성
- 이미 생성된 HTML파일을 받아서 SEO에 친화적

**SSG 단점**

- 모든 URL에 대해 개별 HTML 파일을 생성해야한다.
- URL을 미리 예측할 수 없으면 적용이 어려움

**SSR vs SSG**

- SSR은 SSG에서 가능한 것보다 더 많은 “실시간”데이터를 가져와 보다 완전한 요청에 대한 응답을 하는 것이다.
- 속도는 SSG가 빠름.
- 따라서 필요한 경우에만 SSR을 사용

### Universal Rendering

- SSR을 통해 빠른 FCP를 구현한 다음 클라이언트에서 rehydration이라는 기술을 통해 다시 렌더링하는 방식.
- 초기로딩시 SSR / 그 이후에 CSR로 작동

**Universal Rendering 장점**

- SSR을 통해 빠른 FCP를 구현함으로 CSR의 단점 개선

**Universal Rendering 단점**

- 별도의 서버 필요, 러닝커버 비용 큼

### Incremental Static Regeneration (ISR)

- 런타임 중에 정적 페이지를 만들거나 업데이트 할 수 있도록 해주는 SSG와 SSR의 하이브리드 솔루션
- Next.js에서 제공하는 기능이기도 하며, 전체 사이트를 다시 빌드할 필요없이 페이지별로 정적생성 사용가능하게 해줌

**ISR 동작 방식**

1. 사용자의 웹 페이지 방문 (request)
2. 요청에 의해 페이지가 npm생성되지만 SSR과 달리 즉시 대체 페이지(fallback page)가 제공됨
   1. placeholder 및 스캘래톤 표시
3. 데이터가 확인되면 최종 페이지가 캐시되고 사용자는 SSG와 마찬가지로 캐시된 버전의 페이지를 받음
4. 재검증시에도 사용자는 먼저 캐시된 버전을 받고 업데이트된 버전을 받는다.

**ISR 장점**

- SSR과 달리 페이지가 즉시 제공(fallback page), 좋은 사용자경험

**ISR 단점**

- 페이지 디자인에 따라 첫번째 의미있는 페인팅을 지연시킬 수도 있다.

[SSR, CSR, SSG, TTV, TTI 개념 정리](https://velog.io/@wiostz98kr/SSR-CSR-SSG-TTV-TTI-개념-정리)
