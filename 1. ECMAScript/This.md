# this

## #1 전역(global context)
window 객체를 가리킴    

    > this
    //  Window {0: global, window: Window, self: Window,  
    //  document: document, name: '', location: Location,
    //  ... }


## #2 함수에서의 this
[function 키워드로 선언된 함수](./FunctionRegularOrArrow.md)는 strict 모드의 여부에 따라 다름

### non-strict mode
전역 this, 즉 window를 가리킴

    function func(a,b){ 
        console.log(a+b);
        console.log(this);
        return a+b;
    }
    func(6,66)
    //  VM293:1 72
    //  VM293:1 Window {0: global, window: Window, self:
    //  Window, document: document, name: '', location: 
    //  Location, ...}
### strict mode
문맥 진입 시에 설정되는 값을 유지  

    unction strictFunc(a,b){
        "use strict";
        console.log(a*b);
        console.log(this);
        return a*b;
    }
    strictFunc(6,66)
    //  VM560:1 396
    //  VM560:1 undefined

### this의 값을 다른 문맥으로 넘기는 법
call(), apply()는 인자로 전달된 값(this에 대한)이 객체가 아닌 경우 이를 객체화한다  
- call은 인자를 하나하나 받지만 apply는 인자를 array로 받는다

    //  from [SOF](https://stackoverflow.com/questions/1986896/what-is-the-difference-between-call-and-apply#:~:text=Both%20call%20and%20apply%20the%20same%20way.%20It,the%20arguments%20of%20the%20functions%20as%20an%20array.)  
    func.apply( valueForThis, arrayOfArgs )  
    func.call( valueForThis, arg1, arg2, ... )

### bind()
다른 범위의 this를 함수에서 사용하고 싶을 때 .bind(this)를 통해 새로운 함수를 리턴하여 사용한다

    function f(){
        "use strict";
        console.log(this.innerHeight);
    }
    f()     //  VM788:3 Uncaught TypeError: Cannot read 
            //  properties of undefined (reading 'innerHeight')
            //      at f (<anonymous>:3:22)
            //      at <anonymous>:1:1

    const g=f.bind(this)
    g()     //  VM788:3 763


## #3 객체에서의 this
객체의 메서드 안에서의 this는 그 객체 전체를 가리킨다. 

    //  coordination.ts
    class Coordination{
        private _x: number
        private _y: number
        constructor(x?: number, y?: number){
            this.setCoor(x ?? 0, y ?? 0)
        }
        public setCoor(x:number,y:number){
            this._x=x
            this._y=y
        }
        ...
    }


## #4 DOM 이벤트 처리기
이벤트를 발생시킨 오소에 bind됨

