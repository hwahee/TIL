# REDUX
ref. from [공식 사이트](https://ko.redux.js.org/introduction/getting-started/) 


## 무엇인가?
- 예측 가능한 상태 컨테이너
- 모든 컴포넌트의 상태 관리를 하나의 store에서 관리한다


## 특징과 부품
앱의 상태는 단일 store안의 객체 트리에만 저장됨 - 이 상태 트리를 변경하는 방법은 reducer를 작성하여 action을 보내는 것

### reducer
(state, action)=>state 형태의 순수 함수 - side effect가 일어나지 않음

        const reducer = (oldState = initState, action) => {
        switch (action.type) {
                case 'CHANGE_COLOR':
                return { ...oldState, color: action.color }
        ...
        
spread 연산자를 사용하여 oldState를 바꾸지 않고 값만 복사한 다음 변경을 원하는 값만 변경하여 리턴한 형태

### slice
함수 목록에 있는 함수들이 자동으로 리류서와 state에 상응하는 action으로 만들어진다

### selector
state에 있는 요소 중 특정한 것만 필요할 경우 사용할 수 있다

        useSelector((state: RootState) => state.counter.value)


## 효과
- action에 따른 상태의 변경 사항을 추적할 수 있음 -> 디버그 시 시간 순으로 변화를 추적하는 것이 가능함
- undo, redo가 쉬움
- side effect가 일어나지 않음 -> 테스트 시 일어날 수 있는 문제가 줄어듦


## redux가 없다면?
특정 컴포넌트에서 발생한 상태변화가 다른 떨어진 컴포넌트에게 영향을 주려면
- 공통의 부모까지 거슬러 올라간 다음 해당 컴포넌트까지 타고 내려가야 한다
- 이 때 타고 내려가기 위해서 중간에 있는 컴포넌트들에 props를 추가해줘야 하는 문제가 생긴다(Props Drilling Problem) 
> redux는 이러한 상태변화를 reducer를 사용하여 처리한 다음 이에 따르는 영향을 store 안에서 직접 관리하도록 한다


