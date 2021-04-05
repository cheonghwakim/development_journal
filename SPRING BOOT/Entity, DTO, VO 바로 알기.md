스프링부트 프로젝트를 진행하면서 JPA를 사용하게 되었다. MyBatis를 쓸 때는 개념적으로 DTO, VO가 그냥 데이터 객체들을 옮겨다 주는 통 정도로만 이해했는데, JPA를 사용하면서 Entity, DTO, VO가 뭔가 비슷하면서도 다른 것 같았다... 그렇지만 귀찮아서 넘기고 있다가 확실히 짚고 넘어가는 것이 좋겠다는 생각에 정리해본다..



### 1. Entity

```
Entity 클래스는 실제 DataBase의 테이블과 1:1로 매핑되는 클래스
DB의 테이블 내에 존재하는 컬럼만을 속성(필드)으로 가져가야 한다.
Entity 클래스는 상속을 받거나 구현체여서는 안 되며, 테이블 내에 존재하지 않는 칼럼을 가져서도 안 된다!
```

- 최대한 외부에서 Entity 클래스의 getter method를 사용하지 않도록 해당 클래스 안에서 필요한 로직 method를 구현해야 한다.

#### 1.1 Entity, DTO Class 분리 이유

DB Layer와 View Layer 사이의 역할을 분리하기 위함

**Entity 클래스는 실제 테이블과 매핑되어 만약 변경된다면 여러 다른 클래스에 영향을 끼친다. 반면, DTO 클래스는 View와 통신하며 자주 변경되므로 분리해주어야 한다.**



#### 1.2 Entity Setter 금지 및 생성자, 접근 제어

엔티티를 작성할 때 Setter를 무분별하게 사용하면 객체(Entity)의 값을 변경할 수 있으므로 객체의 일관성을 보장할 수 없다. 객체의 일관성을 유지할 수 있어야 유지 보수성이 올라가기 떄문에 Setter를 사용해서는 안되며, 객체의 생성자에 값들을 넣어줌으로써 Setter 사용을 줄일 수 있다.

```java
// 객체 생성자 설정
@Builder
public Member(String username, String password, String name) {
        this.username = username;
        this.password = password;
        this.name = name;
    }


// 객체 생성 시 값 세팅(빌더패턴 사용)
Member member = Member.Builder()
      .username("name")
      .password("1234")
      .name("name)
      .build();

```



아래와 같이 **기본 생성자 접근 제한자를 protected로 변경**하면 **new Member() 사용을 제한**해 **Entity의 일관성을 더 유지**할 수 있다.

```java
// Member 엔티티
@Entity
@Getter
@Table(name = "member")
public class Member{

    // 기본 생성자 protected로 접근 제한(기본 생성자 접근 제한자는 protected 까지 허용
    //기본 생성자의 접근 제한자를 private으로 걸면, 추후에 Lazy Loading 사용 시 Proxy 관련 예외가 발생)
    protected Member(){};
    
    ...
}


// @NoArgsconstructor 어노테이션을 통한 protected 접근 제어.
@Entity
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@Getter
@Table(name = "member")
public class Member {

}
```



#### 1.3 Entity 예제 코드

```java
@Getter
@Setter
@ToString
@Table(name = "user")
@Entity
public class User {

    @Id
    @GeneratedValue
    private int id;

    @Column(name = "name", nullable = false)
    private String name;

    @Column(name = "password", nullable = false)
    private String password;

    @Column(name = "email", nullable = false, unique = true)
    private String email;

    @Column(name = "phone", nullable = false, unique = true)
    private String phone;

    @Column(nullable = true)
    private LocalDateTime create_date;

    private LocalDateTime modify_date;

}
```





### 2. DTO (Data Transfer Object)

```
Dto는 데이터 전송(이동) 객체라는 의미를 가지고 있다. 주로 비동기 처리를 할 때 사용한다.
```

**계층간 데이터 교환을 위한 객체(Java Beans)**이다.
**DB의 데이터를 Service나 Controller 등으로 보낼 때 사용하는 객체**를 말한다. 즉, **DB의 데이터가 Presentation Logic Tier로 넘어올때는 DTO로 변환되어 오고가는 것**이다.
로직을 갖고 있지 않는 순수한 데이터 객체이며, getter/setter 메서드만을 갖는다.
또한 **Controller Layer에서 Response DTO 형태로 Client에 전달**한다.



#### 2.1 DTO와 VO의 차이점

VO는 DTO와 동일한 개념이지만 read only 속성을 갖는다. VO는 특정한 비즈니스 값을 담는 객체이고, DTO는 Layer간의 통신 용도로 오고가는 객체를 말한다.



#### 2.2 DTO 예제 코드

```java
@Getter 
@Setter
class ArticleDTO {
  private String title;
  private String content;
  private String writer;
}
```



### 3. VO(Value Object)

```
VO(Value Object)는 말 그대로 값 객체라는 의미를 가지고 있다.
VO의 핵심 역할은 equals()와 hashcode() 를 오버라이딩 하는 것이다.
VO 내부에 선언된 속성(필드)의 모든 값들이 VO 객체마다 값이 같아야, 똑같은 객체라고 판별한다.
```

VO는 Getter와 Setter를 가질 수 있다. 테이블 내에 있는 속성 외에 추가적인 속성을 가질 수 있으며, 여러 테이블(A, B, C)에 대한 공통 속성을 모아서 만든 BaseVO 클래스를 상속받아서 사용할 수 있다.



#### 3.1 VO 예제 코드

```java
@Getter 
@Setter
@Alias("article")
class ArticleVO {
    private Long id;
    private String title;
    private String contents;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Article article = (Article) o;
        return Objects.equals(id, article.id);
    }

    @Override
    public int hashCode() {
        return Objects.hash(id);
    }
}
```