- JDBC는 Java Database Connectivity로 DB에 접근할 수 있도록 Java에서 제공하는 API입니다.

- JDBC에 연결해야하는 DB의 JDBC 드라이버를 제공하면 DB 연결 로직을 변경할 필요없이 DB 변경이 가능합니다.
- DB 회사들은 자신들의 DB에 맞도록 JDBC 인터페이스를 구현한 후 라이브러리로 제공하는데 이를 JDBC 드라이버라 부릅니다.

- 커넥션 연결, statement 준비 및 실행, 커넥션 종료 등의 반복적이고 중복되는 작업들을 대신 처리해주는 JdbcTemplate이 등장했습니다.