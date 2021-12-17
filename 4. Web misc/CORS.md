# Cross-Origin Resource Sharing
ref. from [softAuthor](https://softauthor.com/cors-error-solution-in-a-nutshell/), [mdn](https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy)

어느 클라이언트가 어느 도메인에서 접근하든 데이터를 사용할 수 있게 하는 보안 메커니즘  
CORS가 열려있다면 보통은 어떤 도메인에서든 요청하고 응답을 받을 수 있다

## Same Origin Policy
브라우저가 서버와 클라이언트가 같은 영역에 있을 때에만 통신을 허가하는 것(다른 출처에서 가져온 리소스와 상호작용 제한)  
브라우저에서 보안상의 이유로 기본적으로 설정됨

### 같은 출처(영역, 도메인)란 것은 무엇을 의미하는가? 
두 URL의 프로토콜, 명시된 포트, 호스트가 모두 같은 경우 
    
    프로토콜이 다르다(http, https)
    http://example.com/page.html
    https://example.com/page.html
    
    호스트가 다르다
    http://main.example.com/page.html
    http://sub.example.com/page.html

    포트가 다르다
    http://example.com:8080/page.html
    http://example.com:8181/page.html

    성공! (경로만 다를 뿐 나머지는 같다)
    http://main.example.com/page.html
    http://main.example.com/data/infoData.json


## CORS
- 추가 헤더를 서버쪽의 API에 붙여서 CORS 활성화
- 한 출처에서 실행중인 웹 애플리케이션이 다른 출처의 자원에 접근할 수 있는 권한을 부여함

        //nodejs
        app.use((req, res, next) => {
            res.header(
                "Access-Control-Allow-Origin",  
                "YOUR-DOMAIN.TLD"
            )
            res.header(
                "Access-Control-Allow-Headers", 
                "Origin, X-Requested-With, Content-Type, Accept"
                )
            next()
        })




