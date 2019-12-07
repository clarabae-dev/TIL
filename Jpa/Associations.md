### Outline  
JPA에서는 객체로 표현하기 어려운 데이터간 관계를 표현하기 위해 여러 기능을 제공하고 있다.  
JPA에서의 데이터 관계는 크게 단방향과 양방향의 관계로 나뉜다.
단방향과 양방향의 차이는 데이터를 사용하는 관점에서 누가 주도권을 가지는가이다.  
부모 테이블의 PK와 자식 테이블의 FK를 연결해 Entity간 관계를 지정한다.  
> 부모 parent 테이블 PK: id <-> 자식 child 테이블 FK: parent_id  

#### OneToOne (1:1)  
부모 테이블과 자식 테이블의 레코드가 각각 하나씩 연결된다.  
OneToOne 관계 설정에는 FK를 어느 곳에 두어야 하는지 생각해야 한다.  
JPA 상에서는 FK를 갖는 쪽이 주도권을 가지게 된다.  
주도권을 갖는 쪽이 데이터베이스 연관 관계와 매핑되고 FK를 관리(등록, 수정, 삭제)할 수 있기 때문이다.  

#### OneToMany (1:N)  
데이터를 바라보는 주체가 부모 Entity이며 하나의 부모 Entity와 관계를 맺는 N개의 자식 Entity를 사용하겠다는 의미이다.  
- @ElementCollection
자식 Entity의 모든 속성 값을 가지고 오는 것이 아니라 필요한 속성의 값만 가지고와서 Collection으로 구성할 수 있다.  

#### ManyToOne (N:1)  
자식 Entity에서 부모 Entity를 바라볼 때 사용한다.  
ManyToOne FetchType의 기본값은 EAGER로 자식 Entity가 조회됨과 동시에 부모 Entity를 조회한다.  

#### ManyToMany (N:N)  
데이터베이스 상에 표현할 수 없는 관계이며, JPA 상에서 논리적으로만 표현할 수 있다.  
ManyToMany를 표현할 수 있는 맵핑 테이블을 생성해 서로의 PK를 가지고 관계를 설정한다.  

#### Attributes  
- orphanRemoval() default false  
부모 Entity가 테이블에서 삭제되면, 삭제된 부모 Entity와 관계를 맺는 모든 자식 Entity들은 고아가 된다.  
true로 지정하면 부모 Entity가 삭제되었을 때, 자식 Entity들도 삭제된다.   
- cascade  
관계를 맺은 Target Entity에 종속성을 부여한다.  
  - CascadeType: ALL, PERSIST, MERGE, REMOVE, REFRESH, DETACH  
  PERSIST: Entity가 save되면, Target Entity도 save된다. OneToMany에서 주로 사용하는 중.  
- mappedBy  
양방향 관계 매핑이 된다.  
- optional() default true  
관계를 맺는 것이 선택적인가를 지정할 수 있다. false로 지정하면 null이 아닌 관계가 항상 존재해야 한다.  
- fetch  
하나의 Entity를 조회할 때, 관계를 맺은 객체들을 어떻게 가져올 것인가를 나타낸다.  
  - FetchType: LAZY, EAGER  
  EAGER: 관계를 맺은 Entity를 모두 가져온다.  
  LAZY: 관계를 맺은 Entity를 즉시 가져오지 않고, 실제 사용될 때(getter로 접근할 때) 가져온다.  

#### N+1 문제  
OneToMany 양방향 관계에서 부모 Entity를 조회할 때,  
자식 Entity들을 함께 조회하는 것이 아니라, 자식 Entity의 수만큼 추가 조회하는 문제.  
> SELECT * FROM MASTER  
  SELECT * FROM STUDENT WHERE MASTER_ID = 0(MASTER_ID:FK)  
  SELECT * FROM STUDENT WHERE MASTER_ID = 1  
  SELECT * FROM STUDENT WHERE MASTER_ID = 2  
  SELECT * FROM STUDENT WHERE MASTER_ID = 3 ...  

- Join Fetch  
조회할 때 바로 가져오고 싶은 Entity 필드를 지정하는 방법.  
> @Query("select a from Academy a join fetch a.subjects")  
  List<Academy> findAllJoinFetch();  
> 자식 Entity의 자식 Entity까지 한번에 가져와야 할 때 join fetch 쿼리문.  
  @Query("select a from Academy a join fetch a.subjects s join fetch s.teacher")  
  List<Academy> findAllWithTeacher();  

- Entity Graph  
attributePaths에 쿼리 수행시 바로 가져올 필드명을 지정하면 Lazy가 아닌 Eager 방식으로 조회한다.  
> @EntityGraph(attributePaths = "subjects")  
  @Query("select a from Academy a")  
  List<Academy> findAllEntityGraph();  
