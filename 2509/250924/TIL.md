### Spring Security 6.1 이후 변경점
```
.authorizeRequests() → .authorizeHttpRequests() 
.antMatchers() → .requestMatchers()
.access("hasAnyRole('ROLE_A','ROLE_B')") → .hasAnyRole("A", "B")
```

메서드 체이닝이 사라지고 람다식을 통해 함수형으로 설정

## 분산 추적
Metric : 상태, 성능, 안정성을 나타내는 지표

### Micrometer
- Spring 기반 애플리케이션에서 메트릭을 수집하고 모니터링하기 위한 라이브러리
- 다양한 메트릭 수집, 유연한 연동(Prometheus, Grafana)
    1. 수집된 메트릭을 보관할 DB ( = 프로메테우스 )
    2. 수집된 메트릭을 시각화 할 대시보드 ( = 그라파나 )
- 추적 기능

### Zipkin
- 트레이스 데이터: 개별 요청(트랜잭션)의 흐름을 따라가는 데이터
- 트레이스 데이터를 수집하고 시각화하는 분산 추적 시스템
- 시각화, 검색 및 필터링 제공