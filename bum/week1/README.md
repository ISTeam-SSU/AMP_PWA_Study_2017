# AMP 정리

## AMP란?

(bold)Accelerated Mobile Page

웹페이지 로딩 속도를 줄이기 위해 기존 HTML 웹페이지의 성능을 저하시키는 것들을 못쓰도록 제약을 건 웹페이지

## AMP의 3요소

  1. AMP HTML

    기존의 HTML 태그와 기존의 태그 앞에 `amp-`를 붙인 태그가 있다

  2. AMP JS

  3. AMP CACHE

## 제약 사항 및 특징
```
  1. 비동기 스크립트만 허용
    * author-written js는 포함 못시키고 그 대신에 custom amp element로 js 코드를 직접 작성할 수 있다
    * third party js는 iframe에서 혀용
      `Q1. third party js vs author-written js를 amp가 어떻게 구분?`
  2. 모든 리소스의 사이즈를 정해줘야한다

  3. 확장 메커니즘이 렌더링을 차단하지 않도록 한다
      * 인스타, 트위터 같은거 추가해도 성능에 지장x
  4. 모든 타사 Js를 주요 경로에서 제거한다

  5. 글꼴 트리거는 효율적이어야 한다

  6. css는 inline으로만 작성할 수 있으며 최대 50kb까지 작정 가능하다
    `Q2. In AMP pages, all DOM reads happen first before all the writes 의미 (0.0)?`

  7. GPU 가속 애니매이션만 사용한다

  8. 리소스 로드의 우선순위를 지정한다

  9. 즉시 페이지 로드
```
## TUTORIAL NOTES

  ### 첫번째 AMP 페이지 만들기
```
    꼭 해야하는 것
      1. <!doctype html>로 시작
      2. <html amp> 태그가 꼭 있어야 한다
      3. <head> 또는 <body> 태그가 꼭 있어야한다
      4. <link rel="canonical" href="$SOME_URL"> 태그 꼭 있어야 한다.(SOME_URL은 일반 html버젼 링크 OR 자기 자신 링크)
      5. <head>의 첫 자식 태그로 <meta charset="utf-8"> 있어야 한다
      6. <meta name="viewport" content="width=device-width,minimum-scale=1"> 가 <head>태그 내에 있어야 한다
      7. <script async src="https://cdn.ampproject.org/v0.js"></script> 가 <head> 태그 내에 있어야 한다
      8. <style>{{공식 홈페이지에 있는 css}}</style> 추가
```
  ### INCLUDE A image

    <img>태그 대신에 <amp-img>태그 사용 (이 외에도 몇몇 태그는 앞에 amp-붙여야만 사용 가능)

  ### MODIFY PRESENTATION AND LAYOUT

    inline css만 쓸 수 있다

  ### PREVIEW AND VALIDATE

    로컬 서버 킨 뒤 localhost/{{path to amp.html}}#development=1에 접속하면 콘솔로 에러를 확인할 수 있다

  ### LINKING AMP-일반 HTML

```
    <head> 내에 <link rel="canonical" href="$SOME_URL">로 AMP-일반 HTML을 link할 수 있다
      1. AMP-일반 HTML을 link할 경우 AMP에서 href에 일반 HTML주소를, HTML주소에서 href에 일반 AMP주소를 적으면 된다
      2. 둘 중 한 버젼만 있으면 href에 자기 자신의 주소를 적는다
```

  ### 로그인

    * amp-access 태그로 인증 여부를 판별한다
```
    과정
      1. 로그인 버튼을 클릭하면 AMP 런타임이 request url에 자동으로 return parameter을 추가한다
      2. 서버에서 응답을 받는다
      3. AMP 런타임이 로그인 창을 닫고 returnURL로 리다이렉트 시킨다
```
  ### 댓글 추가
```
    1. amp-form 라이브러리를 사용한다
    2. amp-form은 post 시 xhr요청만 허용한다
    3. post 요청 성공하면 submit-success, 실패하면 submit-error
    4. xhr요청을 보내면 서버로부터 댓글 정보가 json으로 온다
    5. amp-mustache로 댓글 정보 표시
```
  ### 로그아웃
```
    과정
      1. 로그아웃 버튼을 클릭하면 AMP 런타임이 request url에 자동으로 return parameter을 추가한다
      2. 서버에서 응답을 받는다
      3. AMP 런타임이 returnURL로 리다이렉트 시킨다
```

  ### 라이브 블로그 만들기
  ```
    1. amp-live-list 활용
      `Q3. 폴링하는 호스트 문서 주소는 어디에 입려?`
  ```
  ## MORE

* AMP Events & Actions link: https://github.com/ampproject/amphtml/blob/master/spec/amp-actions-and-events.md
