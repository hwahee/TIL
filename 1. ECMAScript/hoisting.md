# 호이스팅
컨텍스트 내에서 번수의 선언을 최상단으로 끌고오는 것

## var로 변수를 선언할 때의 효과(호이스팅)
- JS에서는 변수가 선언되기 전에 할당되어도 유효하다. 이는 JS 인터프리터가 코드를 읽을 때 var를 이용한 변수의 선언을 컨텍스트의 최상단으로 끌고 오기 때문이다
- 이는 컨텍스트 내에서 함수가 선언될 때 유용하다. 위에서 아래로 절차적으로 코드를 해석할 때 나타나는 전방 선언 문제가 해결되기 때문이다
  

## var의 문제점
- var 키워드에 의해 호이스팅된 변수는 최상위로 옮겨졌을 때 선언과 동시에 초기화되지 않았다면 기본적으로 undefined로 초기화된다
- 이는 실수로 잘못된 값으로 인해 오류를 내야 할 때에도 잘못된 방법이지만 어떻게든 실행시키기 때문에 오류를 찾기 힘들게 하는 부작용을 낳았다


## var와 let의 차이
- let은 var와 다르게 컨텍스트의 맨 처음에서 undefined를 할당하지 않는다
- 따라서 let 키워드를 만나 선언되기 전에 사용된 변수에 대해서 참조 에러를 내기 때문에 오류를 발견하기 쉽다
  
## 코드
    function f(){
        x=14
        console.log(x)
        return    

        var x=0
    }
    f()    // VM892:3 14    undefined
    
    function g(){
        y=44
        console.log(y)
        return

        let y=0
    }
    g()     //VM921:2 Uncaught ReferenceError: Cannot access 
            //'y' before initialization
            //at g (<anonymous>:2:6)
            //at <anonymous>:1:1

## 기타
- ES6에서 let 키워드가 추가되었고, var는 현업에서 쓰이지 않게 되었다
- ()=>{} 문법을 사용하는 함수(arrow function)는 거의 대부분 const로 선언과 동시에 할당된다