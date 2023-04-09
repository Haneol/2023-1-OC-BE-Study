## 의존과 의존성

### 의존성(Dependency)이란?

- 코드에서 두 모듈(클래스) 간의 연결 혹은 관계를 의미
- 클래스 A가 다른 클래스 B를 이용할 떄 A가 B에 의존성을 지닌다고 말한다
    - A는 B 없이 작동할 수 없다
    - 클래스 B가 변하면 A에도 영향을 미친다.
- 저수준 → 고수준 정책을 향해야함
    - 고수준 : 추상화된 개념
    - 저수준 : 추상화된 개념을 실제 어떻게 구현할지에 대한 세부적인 개념
- 즉, 구체적인 것이 추상화된 것에 의존해야 한다.

### 의존성을 지양해야하는 이유

- 높은 의존성은 모듈의 재사용을 감소시킴
- 모듈이 바뀌면 그 모듈에 의존하는 다른 모듈까지 변경이 이루어짐
- 테스트 시 유닛 테스트 작성이 어려움

## @Autowired 의존성 주입

### 의존성 주입(DI : Dependency Injection)

- 객체가 의존하는 또 다른 객체를 외부에서 선언하고 이를 주입하는 것
- 하나의 패턴으로 의존성들을 인자들로 전달해준다면 모듈안에서 의존성을 불러오거나 새로 만드는 것을 피할 수 있음

### 의존성 주입의 이점

- 의존성이 줄어든다
- 재사용성을 높일 수 있다
- 테스트하기 좋은 코드가 된다
- 가독성이 좋아진다

### 의존성 주입의 3가지 방법

- 생성자 주입(Constructor Injection)
- 필드 주입(Field Injection)
- Setter 주입(Setter Injection)

### @Autowired

- 주입하려고 하는 객체의 타입이 일치하는 객체를 자동으로 주입
- 필드, 생성자, Setter에 붙일 수 있다
- 단, 필드, Setter에 붙여서 사용할 경우 반드시 기본 생성자가 정의되어 있어야 한다

### 권장 주입 방식

- Spring에서는 생성자 주입을 권장함
- 생성자 주입을 권장 하는 이유
    - 순환 참조 방지
    - 불변성
    - 테스트에 용이

## DIP

### 의존 관계 역전 원칙(DIP : Dependency Inversion Principle)

- 객체 지향 프로그래밍 설계의 5대 기본원칙(SOLID) 중 마지막 원칙
- 상위 계층(정책 결정)이 하위 계층(세부 사항)에 의존하는 전통적인 의존관계를 반전
→ 상위 계층이 하위 계층의 구현으로부터 독립되게 하는 것
- 즉, 자주 변화하는 것에 의존하기 보다는 변화하기 어려운 것 또는 거의 변화가 없는 것에 의존하라는 원칙

### DIP의 이점

- 종속성이 줄어듦
- 유지관리 및 쉬운 코드 작성이 가능

## 스프링 빈과 스프링 컨테이너란?

### 스프링 컨테이너

- Spring에서 자바 객체들을 관리하는 공간
- 자바 객체를 Spring에서는 빈(Bean)이라고 하는데, 스프링 컨테이너는 빈의 생성부터 소멸까지를 개발자 대신 관리 해줌
- 크게 두 종류가 존재
    - BeanFactory
        - 빈을 등록하고 생성하고 조회하고 돌려주는 등 빈을 관리하는 역할
    - ApplicationContext
        - BeanFactory와 마찬가지로 빈을 관리할 수 있음
        - BeanFactory의 빈을 관리하는 기능을 상속받았으며, 부가적인 기능이 더욱 추가되어있으므로 → 보통의 경우 스프링 컨테이너를 ApplicationContext로 사용

### 스프링 빈

- Spring에서는 자바 객체를 빈(Bean)이라고 함
- 보통의 경우 스프링 컨테이너에 빈 인스턴스를 단 한개만 저장하는 싱글톤 패턴을 채택
- 빈 이름은 항상 다르게 지정되어야 함

## JDBC와 JPA?

### 영속성(Persistence)

- 프로그램이 종료되더라도 사라지지 않는 데이터의 특성
- Persistence Layer는 프로그램 아키텍처에서 데이터에 영속성을 부여해주는 계층을 말함
    - Persistence framework를 주로 이용
        - JDBC 프로그래밍의 복잡함이나 번거로움 없이 간단한 작업으로 데이터베이스와 연동되는 시스템을 빠르게 개발할 수 있음
        - SQL Mapper
            - SQL query문을 통해 직접 데이터베이스를 다룸
            - Mybatis, JdbcTemplate이 존재
        - ORM
            - 데이터베이스 객체를 자바 객체로 매핑
            - SQL query문을 작성할 필요가 없음

### JDBC(Java Database Connectivity)

- DB에 접근할 수 있도록 Java에서 제공하는 API
- Plain JDBC와 Spring JDBC가 존재
- 모든 Persistence Framework는 내부적으로 JDBC API를 사용함

### JPA(Java Persistent API)

- Java ORM 기술에 대한 표준 명세로 Java에서 제공하는 API
- 즉, ORM을 사용하기 위한 표준 인터페이스를 모아둔 것
- JPA의 구성요소
    - javax.persistence 패키지로 정의된 API 그 자체
    - JPAL(Java Persistence Query Language)
    - 객체/관계 메타데이터
- 대표적인 구현체
    - Hibernate, EclipseLing, OpenJPA 등
    - 이런 구현체들을 ORM Framework라 부른다.
