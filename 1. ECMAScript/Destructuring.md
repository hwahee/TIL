# 구조 분해 할당 Destructuring

배열이나 객체의 속성을 해제하여 개별 변수에 그 값을 담는 표현식


## ☆그동안 궁금했던 점과 해답

'let [a,b]=func()' 과 'let {a,b}=func()'의 차이는 무엇인가?

> 구조 분해 할당의 대상(func의 리턴값)이 array인가 object인가에 따른 차이


## 배열 구조 분해 할당

- 일반적인 배열 구조 분해 할당과 spread 연산자를 활용한 변수 선언

    ![array destructuring](https://user-images.githubusercontent.com/44242823/145701133-580ead29-fe39-4145-ad8a-5821ca22fb83.png)

- 함수가 배열을 반환하게 하여 구조 분해 할당하기

        function f(){ return [2,4,6,7] }
        let [a,b,...rest]=f()
        console.log(a,b,rest)    //2 4 (2) [6, 7]


## 객체 구조 분해 할당

    - 객체 구조 분해 할당은 기본적으로 오브젝트 내 속성의 이름을 그대로 변수로 사용해야 한다
    - 만약 다른 이름의 변수가 선언되었다면 해당 변수는 undefined로 초기화된다. 이 때 = 연산자를 사용하여 디폴트 값을 성정해줄 수 있다
    - 변수의 이름을 다른 것으로 하고 싶다면 : 연산자를 사용하여 새로운 이름의 변수에 값을 할당할 수 있다
    - :과 =은 이 순서대로 함께 쓰일 수 있다

- 객체를 반환하는 함수를 사용하여 구조 분해 할당하기

        function f(){ return {a:123, b:"qwe", c:true} }

        let {a, b}=f()
        console.log(a,b)    // VM719:1 123 'qwe'
        
        let {a:myNumber, c:myBoolean}=f()
        console.log(a,c)    // VM874:1 Uncaught ReferenceError: 
                            // c is not defined
                            // at <anonymous>:1:15 
                            // (익명) @ VM874:1
        console.log(myNumber, myBoolean)    // VM1039:1 123 true

- 객체에 없는 이름의 변수 초기화하기와 디폴트 값 사용하기
    
        function f(){ return {a:123, b:"qwe", c:true} }

        let {x,y,c}=f()
        console.log(x,y,c)  // VM1241:1 undefined undefined true
        
        let {i=10, j:jonghyun="Jonghyun Park"}=f()
        console.log(i,jonghyun) // VM1394:1 10 'Jonghyun Park'

- ☆함수 매개변수의 옵션으로 객체를 넣기
    
    빈 객체를 매개변수의 default로 할당함으로써 옵션 object가 주어지지 않으면 모두 디폴드 값으로, 주어진다면 매칭되는 것 이외에는 default값으로 설정할 수 있다
        
        function makeCube({
            width=1,
            height=1, 
            depth=1, 
            color="white"
            }={}){
                console.log( `The volume of the ${color} cube is ${width*height*depth}` ) 
                }

        makeCube({height:6, color:"brown"})
        // VM1203:1 The volume of the brown cube is 6


## 다른 언어에서의 비슷한 표현식

- in python

        (x , y) = (1 , 2)
        print(x + y) #3



