# Annotation 정리

@MappedSuperclass : JPA Entity 클래스들이 Base Time Entity를 상속할 경우 필드들도 칼럼으로 인식하도록 함
@EntityListeners(AuditingEntitListener.class) : BaseTimeEntity 클래스에 Auditing 기능을 포함시킨다
@CreatedDate : Entity가 생성되어 저장될 때 시간이 자동 저장됨
@LastModifiedDate : 조회한 Entity의 값을 변경할 때 시간이 자동 저장됨

---
__reference__
- 스프링부트와 AWS로 혼자 구현하는 웹서비스
