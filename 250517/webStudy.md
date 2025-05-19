| 구분     | HTTP Basic                   | Bearer (JWT)                       |
| ------ | ---------------------------- | ---------------------------------- |
| 방식     | ID + PW를 매 요청 헤더에 Base64로 전달 | JWT 토큰을 헤더에 전달                     |
| 상태     | Stateless (보통 세션 없음)         | Stateless (완전히 서버 세션 없이 JWT만으로 인증) |
| 보안     | HTTPS 필수 (ID, PW 노출 위험)      | HTTPS 필수 (토큰 탈취 위험)                |
| 사용자 UX | 브라우저 기본 팝업 불편                | 클라이언트 앱, SPA 친화적                   |
| 사용처    | 내부 API, 간단 테스트               | 모바일 앱, SPA, Microservice API 인증    |

# SPA
초기 한번만 HTML 페이지를 불러온 뒤, 페이지 전환 없이 필요한 부분만 JavaScript로 동적으로 바꿔주는 웹 앱 구조

✔ 왜 JWT (Bearer)와 SPA가 잘 어울릴까?

SPA에서는
매번 새로고침 없이 API만 호출

서버 세션 관리 없이 클라이언트가 JWT를 저장하고 헤더에 Bearer로 붙여서 API 호출

그래서 SPA에서는 Bearer 인증(JWT)이 많이 사용된다.
