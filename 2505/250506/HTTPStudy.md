# HTTP 1.0
- 헤더 도입
- 응답에 상태코드 추가
- Content-Type 도입 HTML 이외 문서 전송 가능
### 한계
- 커넥션 하나당 요청 하나와 응답 하나만 처리 가능

# HTTP 1.1
- Keep-Alive: TCP연결을 끊지 않고 재사용
- Pipelining: 앞 요청의 응답을 기다리지 않고 순차적으로 요청을 보내고 그 순서에 맞춰 응답을 받는 방식
### 한계
- Head of Line Blocking(HOL): 앞 요청의 응답이 너무 오래 걸리면 뒷 요청은 Blocking된다.
- Header 중복: 연속된 요청의 헤더 많은 중복이 발생

# HTTP 2.0
- Binary Framing 계층
  1. Frame: HTTP 2.0에서 통신의 최소 단위, Header나 Data가 들어있다.
  2. Message: 요청과 응답의 단위이고 다수의 Frame으로 이루어짐.
  3. Stream: 연결된 Connection 내에서 양방향으로 Message를 주고받는 흐름. ID가 있음.
  - Message를 Frame 단위로 분할하며, Binary(이진)로 인코딩. 바이너리 형식 사용으로 파싱속도 및 전송 속도가 빠르고 오류 발생 가능성이 낮아졌다.
  - HTTP1.1은 텍스트 기반 프로토콜
- Multiplexing: 여러 개의 HTTP 요청과 응답을, 하나의 TCP 연결(Connection) 안에서 동시에 처리할 수 있도록 하는 기술. 응답이 요청의 순서에 상관없이 Stream으로 주고 받아 HOL 해결(병렬 처리).
- Stream Prioritization: 리소스간 우선순위를 설정해 클라이언트가 먼저 필요한 리소스부터 보내준다.
- Server Push: 서버는 클라이언트가 요청하지 않았지만 추가적으로 필요한 리소스를 보내줄 수 있다. 캐시에 저장.
- Header Compression: HPACK 압축 알고리즘 사용. Header Table(Static, Dynamic)과 호프만 인코딩 기법을 사용해 압축하여 전송 효율 상승.

# HTTP 3.0
- QUIC: UDP 기반 전송 프로토콜