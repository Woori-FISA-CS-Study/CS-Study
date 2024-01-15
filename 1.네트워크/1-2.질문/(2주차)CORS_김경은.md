# 3️⃣ CORS

## 🫧 SOP 와 CORS

- `SOP`(Same Origin Policy) : 웹브라우저의 보안정책. 다른 출처에서 자원에 접근하는 것을 막음
- `CORS` (Cross Origin Resource Policy) : 교차 출처에서의 자원 접근을 허용해주는 정책

기본적으로 SOP가 적용되어 다른 출처로부터의 접근이 금지되어 있어 이때 접근을 허용하는 방법이 CORS를 적용하는 것이다.

웹브라우저의 정책이므로 서버와 서버의 통신과정에서는 CORS에러가 생기지 않는다.

또한 웹개발이 아닌 앱개발에서도 CORS에러가 없다.

## ✈️ CORS 동작 과정

1. **Prefilght Request**

본 요청을 보내기 전에 접근이 가능한 출처인지 확인하기 위해 미리 보내는 요청

`OPTIONS` HTTP METHOD를 사용하여 전송

<img width="1396" alt="스크린샷 2024-01-13 오후 8 56 03" src="https://github.com/KangHayeonn/together-party-tonight-server/assets/73164845/588f5531-0a41-4343-aa4d-8d39cbe5211c">


**클라이언트**는 헤더에

- `Acess-Control-Request-Method` : 본 요청에서 사용할 http method
- `Access-Control-Request-Headers` : 본 요청에서 사용할 헤더 종류

를 담아 보냄.

**서버**는 응답으로 200번대 http status code를 보내고

헤더에

- `Access-Control-Allow-Origin` : 자원에 접근을 허용할 origin
- `Access-Control-Allow-Method` : 사용가능한 http method 종류
- `Access-Control-Allow-Headers` : 사용가능한 헤더 종류

를 담아 응답한다.

1. **Credential Request**

Preflight Request에 해당하는 조건 +  *인증 정보*가 들어가 있을경우 credential request

인증정보란? 쿠키나 토큰같은 사용자에 대한 정보. `Authorization`이나 `Cookie` 헤더에 담아 보낸다.

동작 방식은 preflight 요청과 동일하다.

1. **Simple Request**

특정 조건에 해당하는 경우 바로 본요청을 보내는 simple request( 잘 사용되지 않음)

- GET, HEAD, POST 중 하나를 사용
- 기본 헤더 외에 직접 추가한 헤더가 `Accept`, `Accept-Language`, `Content-Language`, `Content-Type` 에만 속할 때
- Content-Type 헤더의 값이 다음의 값 중 하나일 때 : `application/x-www-form-urlencoded`, `multipart/form-data`, `text/plain`

## 🍏 해결 방법

1. 서버 측에서 응답 헤더 설정

   `Access-Control-Allow-Origin`

   `Access-Control-Allow-Credentials`

   `Access-Control-Allow-Method`

   `Access-Control-Allow-Headers`

   `Access-Control-Allow-Max-Age` : preflight 요청에 대해 캐싱할 수 있는 최대 시간. 시간 내에 같은 리소스에 재접근 시도 시 preflight 요청 생략

2. 프록시 서버 구축

   서버와 서버 사이의 통신에는 브라우저가 관여하지 않기 때문에 중간에 프록시 서버를 구축하여 해결할 수 있다.

# 🫣 면접 예상 질문
1.  CORS에러를 어떻게 해결할 수 있는지 말해보세요
2.  CORS에러가 왜 일어날까요?