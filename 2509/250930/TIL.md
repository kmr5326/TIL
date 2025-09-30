### @toString 순환 참조 문제
양방향 연관관계에서 toString()이 양쪽 필드 모두 출력하려 하면 무한 순환을 통해 StackOverflowError가 발생한다.
```java
@Getter
@ToString(onlyExplicitlyIncluded = true)
@Entity
class Member {
  @Id Long id;
  @ToString.Include String name;

  @OneToMany(mappedBy = "member")
  @ToString.Exclude               // 🔴 순환 방지
  private List<Order> orders = new ArrayList<>();
}
```

### Entity에 @Setter를 달면 안되는 이유
1. 양방향 연관관계 일관성이 깨진다.
    - 전용 메서드로 두 쪽을 함께 갱신해야 안전
2. 식별자/감사 필드 변경 가능성
    - id(PK) 변경으로 DB 무결성이 깨질 수 있다.
    - createdAt, modifiedAt 등 감사 로그 왜곡