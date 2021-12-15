# 브라우저 렌더링
ref. from [LogRocket](https://blog.logrocket.com/how-browser-rendering-works-behind-scenes/)

## 용어
- Browser Engine
> HTML 문서와 다른 자원들을 화면에 그려주는(render), 브라우저의 핵심 소프트웨어

- DOM: Document Object Model 
> HTML의 부분을 나타내는 객체로써의 노드로 구성된 트리 구조 모델


## 과정
### #1 서버로부터 이진 형식의(raw) 데이터를 받음
### #2 raw 데이터를 가공하여 HTML DOM을 생성
- byte단위의 원 데이터는 문자(character)로 먼저 변환됨
- 다음으로 문자로 변환된 데이터는 토큰으로 나뉘어짐(Tokenization)
  - 토큰: 문자 데이터들이 정보를 담고 있는(의미있는) 단위로 분리된 것
- 토큰들은 다시 노드로 변환됨
- 노드는 트리 구조로 링크가 이루어짐
### #3 css를 링크함 
- css도 위와 같은 과정을 거쳐 최종적으로 CSSOM으로 변환됨
### #4 DOM과 CSSOM이 합쳐져 렌더 트리가 됨
### #5 오브젝트의 위치와 크기를 계산하여 화면에 그려줌


## 자바스크립트의 개입
브라우저가 script 태그를 만나면 DOM의 생성은 스크립트의 실행이 끝날 때까지 일시중지됨
> 자바스크립트는 DOM을 변경할 수 있기 때문 
