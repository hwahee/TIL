# 브라우저의 저장소

## 예시
    //localStorage를 sessionStorage로 바꿔도 같음

    window.localStorage.setItem("items",
        JSON.stringify([{
            id:"3624-qcwdui-f73824h", 
            name: "참치", 
            price:10000, 
            temperature:-15,
        }])
    )

    window.localStorage.getItem("items")
    //  '[{"id":"3624-qcwdui-f73824h","name":"참치",
    //  "price":10000,"temperature":-15}]'
    
    JSON.parse(window.localStorage.getItem("items"))
    //  [{…}]
    
    JSON.parse(window.localStorage.getItem("items"))[0]
    //  {id: '3624-qcwdui-f73824h', name: '참치', 
    //  price: 10000, temperature: -15}

    JSON.parse(window.localStorage.getItem("items"))[0].temperature
    //  -15


## 웹 스토리지
- 웹 페이지에서 생성된 데이터를 간단하게 저장할 수 있는 스토리지
- 간단하게 사용 가능한 대신 유실 가능성이 높음
- key:value 쌍으로, 데이터는 모두 문자열의 형태로 저장됨
    > JSON의 stringify와 parse를 사용해 Object를 string으로 저장하고 저장된 string을 다시 object로 파싱할 수 있다


## 로컬 스토리지와 세션 스토리지
|       |localStorage|sessionStorage|
|-------|------------|--------------|
|생명 주기|동일 브라우저 내에서 지속|세션을 닫으면 소멸|
|공유 범위|같은 주소에서는 여러 탭이어도 하나의 스토리지 사용|각 탭마다 고유한 스토리지를 가짐|


## 쿠키
서버 측에서 클라이언트와 연결될 때 필요한 데이터들을 클라이언트 측에 저장하는 방법
- 최대 4KB의 작은 파일
- HTTP 요청 시 헤더에 자동으로 포함됨
- 유효기간 설정 가능






