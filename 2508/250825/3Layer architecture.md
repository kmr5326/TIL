3 Layer architecture

- controller
  - 클라이언트의 요청을 받습니다.
  - 요청에 대한 로직 처리는 Service에게 전담합니다. Request 데이터가 있다면 Service에 같이 전달합니다.
  - Service에서 처리 완료된 결과를 클라이언트에게 응답합니다.

- service
  - 사용자의 요구사항을 처리 ('비즈니스 로직')
  - DB 저장 및 조회가 필요할 때는 Repository에게 요청합니다.

- repository
  - DB 관리 (연결, 해제, 자원 관리)
  - DB CRUD 작업
