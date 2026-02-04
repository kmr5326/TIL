# 트랜잭셔널 아웃박스 패턴
서비스 로직의 실행과 이벤트 발행을 원자적으로 함께 수행하는 것을 트랜잭셔널 메시징이라고 합니다.
트랜잭션은 커밋됐지만 이벤트 발행은 실패할 수 있으며, 반대로 이벤트 발행은 성공했지만 커밋 연산이 실패하여 트랜잭션은 롤백 될 수 있습니다. 이러한 이중 쓰기로 인해 데이터 정합성에 문제를 만들거나 서비스 장애로 이어질 수 있습니다.

이벤트를 저장하기 위한 Outbox 테이블을 만들고, 같은 트랜잭션 내부에서 이벤트를 저장합니다. 별도의 프로세스가 Outbox 테이블에 저장된 레코드들을 주기적으로 폴링하여 외부 시스템에 성공할 때까지 이벤트를 발행하는 것이 트랜잭셔널 아웃박스 패턴의 구현 방식입니다.
```java
// 예시 코드
@Transactional
public void propagateSample() {
   Product product = new Product("신규 상품");
   productRepository.save(product);
   productOutboxRepository.save(new ProductEvent(product.getId()));
}
```