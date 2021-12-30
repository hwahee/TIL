# SPA vs. MPA


## Multiple Page Application
전통적인 방법

### 동작 방식
클라이언트에서 페이지를 요청하면 서버 측에서 페이지를 구성하여 완성된 페이지를 보내주는 방식

### 특징
- 클라이언트의 상태 변화나 데이터 포스트 등이 있으면 서버는 그것을 반영해 새로운 페이지를 클라이언트에게 보내준다

### 장점
- 검색엔진 최적화에 좋다
  > 완성된 페이지를 받아오기 때문

### 단점
- 페이지 전환이 느리다
- 클라이언트와 서버 간 결합도가 높아진다
  > 서버측에서 어떤 페이지를 전달할지를 클라이언트의 데이터(상태 등)를 바탕으로 결정해야 하기 때문에
- 개발이 복잡해진다
  > 프론트엔드 화면을 구성하기 위해 서버 측에서도 프론트엔드 프레임워크를 알고 있어야 하기 때문에 


## Single Page Application
웹사이트를 네이티브 앱처럼 만들어주는 방법

### 동작 방식
사이트 접속 시 최초로 빈 html 페이지가 로드된다. 이 페이지는 JS API(XHR, fetch 등)를 이용해서 페이지를 채우는 데에 필요한 데이터를 동적으로 로드한다.  

### 장점
- 페이지 전환이 빠르다 
  > 자원이 애플리케이션의 생명 주기에서 최초 한 번만 로드되면 되기 때문에 
- 클라이언트와 서버 간 결합도가 낮아진다, 개발이 단순해진다
  > 서버 측에서 페이지를 렌더하는 코드를 작성할 필요가 없어진다
- 디버그가 쉬워진다
  > 크롬 브라우저로 네트워크의 행동이나 페이지 요소, 데이터 등을 관찰하는 것이 가능하다
- 모바일 애플리케이션을 만들기 좋다
  > 같은 백엔드를 웹과 모바일 두 분야에서 고통으로 사용할 수 있기 때문에
- 웹 스토리지를 사용한 캐싱이 용이하다

### 단점
- 검색엔진 최적화에 나쁘다
  > 구성요소들이 AJAX를 통해 비동기적으로, 새로고침 없이 받아와지기 때문
- 클라이언트 구성요소들을 한번에 필요로 하기 때문에 무겁다
- 보안이 떨어진다
  > 악성 스크립트가 주입되어 클라이언트로 보내질 수가 있다
  