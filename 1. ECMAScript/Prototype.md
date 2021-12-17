# JS의 OOP: 프로토타입

    원형이라 불리는 객체의 복사를 통해 상속(재사용)을 하는 OOP 방법
    인스턴스 기반 프로그래밍


## 프로토타입이란:

- 자바스크립트 객체에서 \_\_proto__ 혹은 [[prototype]] 안에 정의된 것  
![proto examples](https://user-images.githubusercontent.com/44242823/145678953-ae488a0a-0f88-4efa-af88-be49302f5d97.png)


## 프로토타입의 특징

- 구성: prototype object와 prototype link로 이루어짐
    
    - prototype object
        
        일반적인 객체
    
    - prototype link

        객체가 생성될 때 원본이었던 함수의 prototype object를 가리키는 링크
        
        따라서 원본에 정의되어있는 메서드를 복제된 객체에서 실행하면 객체의 \_\_proto__로 링크되어 있는 원본 prototype object의 메서드가 실행됨
        
        
## 프로토타입을 이용한 상속


### 함수를 이용한 오브젝트의 생성

- [regular](./FunctionRegularOrArrow.md) 함수는 new키워드를 통해 construct할 수 있음을 배웠다     


## 다른 언어에서의 프로토타입과 다른 점
    클래래스 기반의 OOP를 지원하는 언어에서의 프로토타입은 여러 인스턴스 간의 공통변수를 설정할 때 쓰인다

