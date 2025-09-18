### 영속성 전이
- CascadeType.ALL : 모든 Cascade 옵션을 적용합니다.
- CascadeType.PERSIST : 엔티티를 영속화할 때, 연관된 엔티티도 함께 영속화합니다.
- CascadeType.REMOVE : 엔티티를 제거할 때, 연관된 엔티티도 함께 제거합니다.
- CascadeType.MERGE : 엔티티 상태를 병합할 때, 연관된 엔티티도 함께 병합합니다.
- CascadeType.REFRESH : 부모 엔티티를 Refresh하면, 연관된 엔티티도 함께 Refresh됩니다.
- CascadeType.DETACH : 부모 엔티티를 Detach하면, 연관된 엔티티도 함께 Detach됩니다.

### 고아 Entity 제거
orphanRemoval = true

### Scheduler
// 초, 분, 시, 일, 월, 주 순서
    
    @Scheduled(cron = "0 0 1 * * *")

@EnableScheduling 달기

### @Transactional
@Transactional이 없으면:

조회 자체는 되지만, 영속성 컨텍스트 범위가 보장되지 않아 Lazy Loading 시 문제가 생김.

사실상 "트랜잭션 바깥"에서 실행되는 것과 같음.

@Transactional(readOnly = true)가 있으면:

조회 트랜잭션을 열어서 Lazy 로딩도 안전하고, 변경 감지도 생략해 성능도 최적화됨.