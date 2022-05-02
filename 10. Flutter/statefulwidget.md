# StatefulWidget


## 요약
- state에 state 변수를 선언할 수 있음
- 위젯이 최초로 생성될 때 initState가 실행됨


## initState, setState
위젯이 최초로 생성될 때 initState가 실행된다. 이 안에서는 주로 변수 최초 값 설정 등이 행해진다.  
이 상태들은 setState 안에서 변화가 일어날 경우 build가 다시 실행되어 화면에 보이는 상태를 바꾼다.  
  
기본적으로 initState는 쵝에 살태를 설정하는 부분이므로 상태를 변화시켜 위젯을 다시 빌드하는 setState를 안에서 쓸 수 없다.

## initState 안에서 setState를 하는 트릭
> Timer(Duration(seconds: 0), callbackFunc) 

Timer 함수를 통해 이벤트를 등록하면 Timer 함수는 주어진 시간만큼 기다린 다음 이벤트를 이벤트 루프에 넣는다. 이때 시간을 0초로 주면 이 함수가 실행되자 마자 바로 이벤트 루프에 주어진 콜백을 등록하는 것이다.  
이렇게 되면 initState 함수 밖에서, initState함수가 완료되자마자 주어진 콜백 함수가 바로 실행되므로 결과적으로 setState를 위젯이 초기화되었을 때 바로 실행하는 효과를 가진다.

