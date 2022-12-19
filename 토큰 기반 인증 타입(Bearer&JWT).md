## TL;DR



### 토큰 기반 인증이란?

쿠키나 세션을 이용한 인증보다 더 보안성이 강하고 효율적인 인증방법입니다.



쿠키를 전달하지않아도 돼서 보안성도 더 좋지만 토큰을 탈취하면 보안에 취약점이 생긴다.

그래서 토큰에 만료기간을 두고 accessToken, refresh Token 개념을 이용한다.



refresh Token도 탈취당하면 그만?

맞다. 하지만 accessToken 은 api 이용 시 마다 노출이되는 반면 refreshToken은 accessToken이 만료됐을 경우만 통신하기때문에 탈취 위험이 accessToken에 비해 적습니다.





### 인증타입

- **Basic** - 사용자 아이디와 암호를 Base64로 인코딩한 값을 토큰으로 사용. (RFC 7617)
- **Bearer** - JWT 혹은 OAuth에 대한 토큰을 사용. (RFC 6750)
- **Digest** - 서버에서 난수 데이터 문자열을 클라이언트에 보냄. 클라이언트는 사용자 정보와 nonce를 포함하는 해시값을 사용하여 응답 (RFC 7616)
- **HOBA** - 전자 서명 기반 인증 (RFC 7486)
- **Mutual** - 암호를 이용한 클라이언트-서버 상호 인증 (draft-ietf-httpauth-mutual)



### 쿠키 인증

- 쿠키는 Key-Value 문자열 덩어리이다.

- 클라이언트의 브라우저에 저장되는 작은 기록정보파일이다.

- 보안에 취약하며 용량제한이 있다.

- 웹 브라우저간 공유가 불가능하다.

  

### 세션인증

- 서버측에 저장하고 관리한다.
- 세션 자체를 탈취하여 서버에 연결할 수 있다.
- 서버에 부하가 심해진다.

### 토큰 인증

- 위 서버 기반 인증 시스템과 달리 상태를 유지하지 않으므로 Stateless 한 특징을 가지고 있다.

- 토큰 자체의 길이가 길어 네트워크 부하가 심해질 수 있다.
- 토큰을 탈취당하면 답이없다.

### JWT (Json Web Token)

HTTP 헤더에 실어 클라이언트를 식별하는 방식이다.

JWT는 Json 데이터를 Base64 URL-Safe Encode 한 것이며 위변조 방지를 위해 개인키를 통한 전자서명도 들어가있다.

구성

헤더 - 페이로드 - 시그니처





`bearer`는 형식에서 인증 타입에 해당합니다. 

Bearer 인증방식에서 JWT 토큰을 이용한 것이겠죠?





레퍼런스

https://velog.io/@cada/%ED%86%A0%EA%B7%BC-%EA%B8%B0%EB%B0%98-%EC%9D%B8%EC%A6%9D%EC%97%90%EC%84%9C-bearer%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C



https://www.okta.com/kr/identity-101/what-is-token-based-authentication/

https://velog.io/@hoo00nn/Token-%EC%9D%B8%EC%A6%9D-%EB%B0%A9%EC%8B%9D%EC%9D%B4%EB%9E%80

https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-JWTjson-web-token-%EB%9E%80-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC#Token_%EC%9D%B8%EC%A6%9D

