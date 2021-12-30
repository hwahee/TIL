# Declare
from [typescript](https://www.typescriptlang.org/docs/handbook/2/type-declarations.html#:~:text=A%20declaration%20file%20provides%20a%20way%20to%20declare,and%20are%20where%20you%E2%80%99d%20normally%20write%20your%20code.)


## 예시
    const k = Math.max(5, 6);
    const j = Math.mix(7, 8);
    // Property 'mix' does not exist on type 'Math'.

### 코드에 Math의 구현 코드가 없어도 어떻게 max와 mix의 존재를 알까?
Math라는 내장 오브젝트의 declaration file이 존재하기 때문에
> declaration 파일은 객체의 실제 구현이 없어도 특정한 타입의 존재를 알려준다


## d.ts 파일
ref. from [SOF](https://stackoverflow.com/questions/21247278/about-d-ts-in-typescript#:~:text=d%20stands%20for%20Declaration%20Files%3A%20When%20a%20TypeScript,interface%20to%20the%20components%20in%20the%20compiled%20JavaScript.)  
- c++의 .h 파일과 유사한 역할을 한다
- js로 작성된 API에 대한 타입 정의를 담고 있다
- js 파일에서 작성된 모듈의 타입을 declare 로 정의한 다음 그것을 export 한다
- js 파일에서 modules.exports로 export된 모듈의 선언을 붙여 export 한다
- 이렇게 export된 모듈은 확장자 없이 import 된다
  
### 예시
    src/
        my-module.js
        my-module.d.ts
        index.ts

my-module.js

    const thing = 42;

    module.exports = { thing };

my-module.d.ts

    export declare const thing: number;

index.ts

    import { thing } from "./my-module"; // <- no extension

    // runtime implementation of `thing` is taken from ".js"
    console.log(thing); // 42

    // type declaration of `thing` is taken from ".d.ts"
    type TypeOfThing = typeof thing; // number