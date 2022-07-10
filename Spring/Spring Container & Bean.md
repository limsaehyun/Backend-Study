# Spring Container & Bean



## Container in Spring

Spring에서는 **Spring Container**, **IoC Container**라는 개념을 사용한다.



### Container

Container는 인스턴스의 생명 주기를 관리하며, 생성된 인스턴스들에게 추가적인 기능을 제공하도록 한다.

- Container - **개발자가 작성한 코드의 처리과정을 위임받은 독립적인 존재**

Container가 적절한 설정만 되어있다면 누구의 도움 없이도 **작성한 코드를 스스로 참조한 뒤 알아서 객체의 생성과 소멸을 컨트롤**한다.



### Spring Container

Spring Container는 **SpringFramework 핵심부에 위치**하며 있으며, **종속 객체 주입(DI)를 이용하여 Application을 구성하는 Component들을 관리**한다.

이때 **Spring Container에서 생성되는 객**체가 `Bean`이다.



### IoC Container

IoC(Inversion Of Control Container) : 제어의 역전

- 기존 구조적 설계와 비교해 프레임워크(Container)가 제어를 나누어 가져가게되어 의존 관계의 방향이 달라지게 되는 것을 **제어가 반전, 역전**되었다고 한다.

IoC(Inversion of Control)를 구현하는 프레임워크로 객체를 관리하고, 객체의 생성을 책임지고, 의존성을 관리하는 컨테이너이다.

- 모두 의존성을 컨테이너(Container)를 통해 받아오기 때문에 개발자가 의도한 대로 구현하기 편하다.

  

## Bean



### Bean의 개념

Bean은 **Spring IoC Container가 관리하는 자바 객체**, **Spring Bean Container에 존재하는 객체**이다.

Spring IoC Container에 의해 객체가 인스터스화, 관리, 생성된다.

Bean Container는 **의존성 주입을 통해 Bean객체를 사용할 수 있도록 해준다.**

Spring Bean은 보통 **Singleton**으로 존재한다.

Spring에서 POJO(Plain Old Java Object)를 Beans라고 부른다.

- POJO : 본래 자바의 장점을 살리는 특정 ‘기술'에 동작하는 것이 아닌 ‘오래된' 방식의 ‘순수한' 자바 객체

Beans는 **Application의 핵심을 이루는 객체**이며, 대부분 **Container에 공급하는 설정 메타 데이터(XML 파일)에** 의해 생성된다.

Container는 **이 메타 데이터를 통해 Bean의 생성, Bean Life Cycle, Bean Dependency(종속성)** 등을 알 수 있다.

***Spring에서의 Bean은 ApplicationContext가 알고있는 객체, 즉 ApplicationContext가 만들어서 그 안에 담고있는 객체를 의미한다.***



### Bean 생성 방식

1. Component Scan

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {

	/**
	 * Exclude specific auto-configuration classes such that they will never be applied.
	 * @return the classes to exclude
	 */
	@AliasFor(annotation = EnableAutoConfiguration.class)
	Class<?>[] exclude() default {};
```

- SpringBootApplication

이 중 CompoenntScan 어노케이션은 sterotype(Service, Controller, Repository 등) **어노테이션이 부여된 class를 찾아 자동으로 Bean으로 등록해주는 역할**을 한다.

ComponentScan을 해주는 범위가 해당 어노테이션이 붙은 위치보다 하위의 class들만 스캔한다. 따라서 **SpringBootApplication의 위치가 가장 상위의 위치**에 있어야 한다.

sterotype을 뜯어보면 내부 구조가 Component가 있는 것을 확인할 수 있다.

추가적으로 Bean으로 등록하고 싶은 class가 있다면 Component 어노테이션을 붙여줘도 상관 없다.

1. Configuration에서 Bean 등록

```java
@Configuration
public class HttpConfig {

    @Bean
    public RestTemplate createRestTemplate(){
        return new RestTemplate();
    }
}
```

Configuration 어노테이션을 사용해서 Bean 어노테노이션을 사용하면 자동으로 빈으로 등록된다.



### Bean Scope

- Spring은 기본적으로 모든 Bean을 Singleton으로 생성하여 관리한다.
- *Singleton Bean*은 *Spring Container***에서 한 번 생성 후**, *Container*가 사라질 때 *Bean*도 제거
- **생성된 하나의 Instance는 Single Beans Cache에 저장**되고, 해당 Bean에 대한 요청과 참조가 있으면 캐시된 객체를 반환한다.
- 하나만 생성되기 때문에 것일한 것을 참조한다. Bean은 Scope가 **명시적으로 지정되지 않으면** **Singleton**이다.
- 구체적으로는 **Application 구동 시 JVM 안에서 스프링 Bean 마다 하나의 객체를 생성하는 것을 의미**한다.
- 그래서 **Spring을 통해서 Bean을 주입 받으면 주입받은 Bean은 동일한 객체라는 가정하에서 개발** 한다.