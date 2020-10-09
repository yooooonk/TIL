# Annotation 정리

- @MappedSuperclass : JPA Entity 클래스들이 Base Time Entity를 상속할 경우 필드들도 칼럼으로 인식하도록 함
- @EntityListeners(AuditingEntitListener.class) : BaseTimeEntity 클래스에 Auditing 기능을 포함시킨다
- @CreatedDate : Entity가 생성되어 저장될 때 시간이 자동 저장됨
- @LastModifiedDate : 조회한 Entity의 값을 변경할 때 시간이 자동 저장됨

### JPA 

- @Entity 
- @GeneratedValue(strategy = GenerationType.IDENTITY) : PK 생성규칙
- @Enumerated(EnumType.String) : Enum 값을 어떤 형태로 저장할지 결정, 기본값은 int

### Lombok
- @Getter
- @Setter
- @NoArgsConstructor : 기본 생성자 자동추가
- @Builder : 해당 클래스의 빌더 패턴 클래스를 생성, 생성자 상단에 선언 시 생성자에 포함된 빌드만 빌더에 제공


---
__reference__
- &#128214; 스프링부트와 AWS로 혼자 구현하는 웹서비스
