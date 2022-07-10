# EJB(Enterprise Java Bean)



# EJB



### Java Bean

Java Bean이란 **자바 객체를 재사용 가능하도록 즉, 컴포넌트화시킬 수 있는 코딩 방침을 정의한 것**을 의미한다.



### EJB

EJB는 [엔터프라이즈급 어플리케이션](https://www.notion.so/Enterprise-Application-Architecture-Pattern-91ba23f15cc34abb90df7c1fa4f20eed) 개발을 단순화하기 위해 발표한 스펙입니다.

개발을 하다 보면 수많은 객체들을 만들게 되는데, 이러한 비즈니스 객체들을 관리하는 컨테이너를 만들어서 필요할 때마다 컨테이너로부터 객체를 받는 식으로 관리하면 효율적이겠다. 라는 논리에서 탄생하게 됩니다.

하지만 서비가 구현해야 한느 실제 비즈니스 로직보다 EJB 컨테이너를 사용하기 위한 상투적인 코드(상속, 구현 클래스 등)들이 너무 많다는 불편함이 있었습니다.

또한, 벤더 사마다 EJB 컨테이너를 구현한 내용이 다르기 때문에 다른 벤더 사의 컨테이너로의 변경의 어려움이 있었고, 이것은 설정이 너무 복잡하다는 문제로 부각되기 시작합니다. 따라서 프로젝트 자체가 특정 기술(개발 툴 등)에 종속. 즉, 기술 침투(Invasive)되는 문제가 발생합니다.



## 이어지는 내용

- [Spring Container & Bean](https://www.notion.so/Spring-Container-Bean-ac0994dc53f44ef5b470abaa3affd139)