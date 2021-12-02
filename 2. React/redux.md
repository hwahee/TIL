# REDUX
ref. from [공식 사이트](https://ko.redux.js.org/introduction/getting-started/) 
## 무엇인가?
- 예측 가능한 상태 컨테이너
- 모든 컴포넌트의 상태 관리를 하나의 store에서 관리한다
## 특징
앱의 상태는 단일 store안의 객체 트리에만 저장됨 - 이 상태 트리를 변경하는 방법은 reducer를 작성하여 action을 보내는 것
### reducer
(state, action)=>state 형태의 순수 함수 - side effect가 일어나지 않음
## 효과
- action에 따른 상태의 변경 사항을 추적할 수 있음 -> 디버그 시 시간 순으로 변화를 추적하는 것이 가능함
- side effect가 일어나지 않음 -> 테스트 시 일어날 수 있는 문제가 줄어듦



