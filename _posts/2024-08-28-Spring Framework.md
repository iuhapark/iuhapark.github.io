---
title: "Spring Bean, Servlet, 제어 역전 (IoC), 의존성 주입 (DI), AOP (관점 지향 프로그래밍)"
date: 2024-08-28 14:15:03 +0900
categories: [Programming, Spring]
tags: [Spring Framework, 객체지향]
math: false
toc: true
pin: true
---
# `Spring Framework`

### Spring Bean

- 스프링 컨테이너는 기본적으로 Bean을 싱글톤으로 관리한다. 그래서 싱글톤 컨테이너라고도 부른다.

스프링 빈은 스프링 빈 컨테이너가 관리하는 순수 자바 객체 **POJO(Plain Old Java Object)**를 의미한다. 순수는 외부 상태에 종속되지 않는 것을 의미한다. 그래서 재활용 하기 좋다. 스프링 빈 컨테이너는 스프링 빈 정의(sping bean definition) 설정을 읽고 스프링 빈 객체를 생성한다. 그리고 서로 의존성이 있는 스프링 빈 객체들을 주입하는 과정을 거친 후 애플리케이션이 실행 준비 상태가 된다.

작업이 끝난 애플리케이션이 종료하기 전 스프링 빈 컨테이너는 관리하고 있던 스프링 빈들의 종료 작업을 실행한다. 이렇게 스프링 빈을 생성하고 소멸하는 전체 과정을 스프링 빈의 생명주기라고 한다. 이때 스프링 빈 컨테이너는 이 생명주기를 관리하는 역할을 한다.

- 어노테이션을 통해 스프링에게 생성 및 관리 책임을 위임함 **제어 역전 (Inversion of Control, IoC)**
    
    ![제어 역전](/assets/img/posts/2024-08-28-1.png)
    
- 자바 설정 클래스 내부(@Configuration)의 @Bean 어노테이션이 붙은 메서드들을 실행하면서 빈 저장소에 실제 빈을 등록
- 가져올 때는 정의한 빈 메서드를 사용한다.

### Servlet

클라이언트의 요청을 처리하고, 그 결과를 반환하는 Servlet 클래스의 구현 규칙을 지킨 자바 웹 프로그래밍 기술

![](/assets/img/posts/2024-08-28-2.png)

![](/assets/img/posts/2024-08-28-3.png)

TCP/IP 연결과 HTTP 요청 파싱, Content-Type 확인 등 위 이미지에서 비즈니스 로직 실행 제외한 모든 단계를 Servlet을 지원하는 WAS가 자동화해준다.

- 클라이언트의 Request에 대해 동적으로 작동하는 웹 어플리케이션 컴포넌트
- Java Thread를 이용하여 동작
- MVC 패턴에서 Controller로 이용됨

서블릿 애플리케이션들을 관리하고 실행하는 서버를 서블릿 컨테이너 또는 [`웹 애플리케이션 서버(WAS - Web Application Server)`](https://iuhapark.github.io/posts/Internet-Network) 라고한다.

서블릿 컨테이너는 서블릿 애플리케이션을 보관하고 사용자 요청에 따라 적절한 서블릿 애플리케이션을 찾아 실행한다.

![HttpServlet](/assets/img/posts/2024-08-28-4.png)

- HTTP 요청 정보를 편리하게 사용할 수 있는 `HttpServletRequest`
- HTTP 응답 정보를 편리하게 제공할 수 있는 `HttpServletResponse`

![Http 요청, Http 응답 흐름](/assets/img/posts/2024-08-28-5.png)

### HTTP 요청, 응답 흐름

- HTTP 요청시
- WAS는 Request, Response 객체를 새로 만들어서 서블릿 객체 호출
- 개발자는 Request 객체에서 HTTP 요청 정보를 편리하게 꺼내서 사용
- 개발자는 Response 객체에 HTTP 응답 정보를 편리하게 입력
- WAS는 Response 객체에 담겨있는 내용으로 HTTP 응답 정보를 생성

### Servelet Container

![Servelet Container](/assets/img/posts/2024-08-28-6.png)

- 톰캣처럼 서블릿을 지원하는 WAS를 서블릿 컨테이너라고 함
- 서블릿 컨테이너는 서블릿 객체를 생성, 초기화, 호출, 종료하는 생명주기 관리
- 서블릿 객체는 **싱글톤으로 관리**
- 고객의 요청이 올 때 마다 계속 객체를 생성하는 것은 비효율
- 최초 로딩 시점에 서블릿 객체를 미리 만들어두고 재활용
- 모든 고객 요청은 동일한 서블릿 객체 인스턴스에 접근
- **공유 변수 사용 주의 (멤버변수)**
- 서블릿 컨테이너 종료시 함께 종료
- JSP도 서블릿으로 변환 되어서 사용
- 동시 요청을 위한 멀티 쓰레드 처리 지원

### DispatcherServlet

스프링 MVC 프레임워크는 프런트 컨트롤러 패턴으로 구현된 **DispatcherServlet**이 클라이언트의 모든 요청과 응답을 처리한다. **DispatcherServlet**은 **사용자의 모든 요청과 응답이 거쳐 가는 곳**이다.

- 
    
    Spring MVC, as many other web frameworks, is designed around the front controller pattern where a central `Servlet`, the `DispatcherServlet`, provides a shared algorithm for request processing, while actual work is performed by configurable delegate components. This model is flexible and supports diverse workflows.
    
    The `DispatcherServlet`, as any `Servlet`, needs to be declared and mapped according to the Servlet specification by using Java configuration or in `web.xml`. In turn, the `DispatcherServlet` uses Spring configuration to discover the delegate components it needs for request mapping, view resolution, exception handling, [and more](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-servlet/special-bean-types.html).
    
    The following example of the Java configuration registers and initializes the `DispatcherServlet`, which is auto-detected by the Servlet container (see [Servlet Config](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-servlet/container-config.html)):
    
    ```java
    public class MyWebApplicationInitializer implements WebApplicationInitializer {
    
    	@Override
    	public void onStartup(ServletContext servletContext) {
    
    		// Load Spring web application configuration
    		AnnotationConfigWebApplicationContext context = new AnnotationConfigWebApplicationContext();
    		context.register(AppConfig.class);
    
    		// Create and register the DispatcherServlet
    		DispatcherServlet servlet = new DispatcherServlet(context);
    		ServletRegistration.Dynamic registration = servletContext.addServlet("app", servlet);
    		registration.setLoadOnStartup(1);
    		registration.addMapping("/app/*");
    	}
    }
    ```
    

### Interceptor와 ServletFilter 설정

### Interceptor

Spring에서의 Interceptor 역할은 Client로부터 들어오는 요청( HttpRequest )을 Controller의 Handler로 도달하기 전에 가로채거나 , Controller로 부터 보내는 응답( HttpResponse )을 가로채는 역할을 한다.

**HandlerInterceptor에서 가로채어 원하는 추가적인 로직을 수행**한 후에 Controller의 Handler로 보낼 수 있도록 하는 Module이다.

개발자가 HandlerInterceptor를 구현하고 설정하면 웹 애플리케이션 전체에 공통 기능으로 확장할 수 있다. 

인터셉터는 서블릿 레벨에서 공통 기능을 제공하는 것이 아니고, 스프링 애플리케이션의 **컨트롤러 클래스 핸들러 메서드 레벨**에서 공통 기능을 제공한다.

### Servlet Filter

**서블릿 스펙**에서도 서블릿 전체에 공통 기능을 추가할 수 있는 기능을 제공하는데, 이를 **서블릿 필터(Servlet Filter)**라고 한다.

DispatcherServlet 앞에서 사용자의 요청과 응답을 처리할 수 있는 구조다. 서블릿 필터는 WAS에서 사용할 수 있는 기술이며, 기능을 웹 애플리케이션에 추가할 때도 WAS에 설정해야 한다. 이때 서블릿 필터는 여러 개 등록 가능하며, 설정을 하면 특정 URI에만 필터 기능을 적용할 수 있다.

![Servlet Filter](/assets/img/posts/2024-08-28-7.png)

### **제어 역전 (Inversion of Control, IoC)**

*개발자는 JAVA 코딩시 new 연산자, 인터페이스 호출, 데이터 클래스 호출 방식으로 객체를 생성, 소멸시킨다.*

객체(인스턴스)의 생성과 소멸 등 개발자가 직접 제어해야 하는 부분들을 프레임워크(정확하게는 컨테이너)가 대신 처리하는 것을 의미. **제어의 주도권**이 개발자에서 **스프링 프레임워크**로 넘어가짐. 그래서 제어의 역전.

IoC가 개발자의 코드를 호출해 필요한 객체를 생성, 소멸 하며 생명주기를 관리하는 것이다.

의존성 역전의 원칙을 패턴화한 것이 제어의 역전(Inversion of Control, loC) 패턴이다. 그리고 패턴을 구현한 구현 방법이 바로 팩토리 메서드, [**디자인 패턴**](https://iuhapark.github.io/posts/Design-Pattern)  서비스 로케이터, 의존성 주입이다.

### **의존성 주입(Dependency Injection, DI)**

프로그램에서 구성 요소의 의존 관계가 소스코드 내부가 아닌 외부의 설정 파일을 통해 정의 되는 방식이다. 스프링 프레임워크에서는 스프링 빈 컨테이너, 즉 ApplicationContext가 이 역할을 담당한다. 스프링 빈 객체들을 생성하고 의존성 있는 스프링 빈들끼리 서로 주입하는 과정을 처리한다. 스프링 프레임워크에서 제공하는 애너테이션을 사용하면 쉽게 주입할 수 있다.

애플리케이션에서 의존성은 반드시 명시적으로(explicity) 선언되어야 하고 분리(isolate)되어 관리되어야 한다. 즉, 의존성 관리 도구와 의존성 선언 파일로 라이브러리 의존성을 관리해야 한다.

메이븐(Maven)은 pom.xml을, 그레이들(Gradle) build.gradle을 사용한다.

### **AOP(Aspect Object Programming, 관점 지향 프로그래밍)**

- 여러 객체에서 공통적으로 사용하고 있는 기능을  관점(aspect) 기준으로 분리해서 모듈화하고 재사용하는 프로그래밍 기법
- 핵심 기능과 공통 기능의 구현을 분리하여 핵심 기능의 코드 수정없이 공통 기능 적용 가능

관점은 여러 클래스에 결쳐 공통으로 실행되는 기능을 모듈로 분리한 것이다. **객체 지향 프로그램밍**에서도 기능에 따라 클래스를 분리하여 작성할 수 있고, 공통으로 기능을 클래스로 분리할 수 있다. 그리고 클래스는 다른 클래스의 메서드를 호출하는 형태를 갖는다. 이때 객체 지향 프로그래밍에서는 클래스가 다른 클래스에 의존한다고 한다. 의존하는 클래스 숫자가 많아지면 그와 비례하여 프로그램 복잡도가 높아진다.

객체 지향 프로그래밍은 의존하는 클래스의 메서드를 직접 호출해야 하지만, **관점 지향 프로그래밍**은 프레임워크의 도움을 받아 코드를 조립할 수 있다. 그래서 클래스의 코드와 관점의 코드를 완전히 분리할 수 있다. 다시 말하면 개발자는 코드를 작성할 때 명시적으로 관점 객체를 생성하지 않으며, 또한 메서드도 직접 호출하지 않는다. 단지 관점이 구현된 클래스에는 대상 클래스의 특정 부분에 기능을 추가하거나 관여할 수 있는 설정이 있을 뿐이다.

이렇게 클래스 밖에서 관점의 기능이 실행되므로 서로 완전히 분리된 형태를 '관심의 분리 (eparation of concers)'라고 한다. 분리된 관심은 애플리케이션에서 클래스의 특정 기능이 실행될 때 모듈화된 관점의 기능과 함께 같이 실행된다. 그러나 클래스 없이 관점만 따로 실행될 수 없다.

클래스의 기능에 관점의 기능을 더하는 형태이므로 관점 지향 프로그래밍이 객체 지향 프로그래밍을 보완한다.

> **장점**
로깅, 트랜잭션, 보안 등 여러 모듈에서 공통적으로 사용하는 기능을 분리하여 관리 할 수 있다.
중복된 코드를 최대한 배제하는 방법으로 가독성과 효율성이 좋다.
여러 객체에 공통으로 적용할 수 있는 기능을 구분함으로써 재사용성을 높여주는 프로그래밍 기법이다.
> 

### **POJO(Plain Old Java Object)**

POJO란 Plain Old Java Object의 약자로, 이를 직역하면 순수한 오래된 자바 객체이다.즉, Java로 생성하는 순수한 객체를 뜻한다.

이를 해석하면 POJO는 객체 지향적인 원리에 충실하면서 환경과 기술에 종속(의존)되지 않고, 필요에 따라 재활용될 수 있는 방식으로 설계된 오브젝트를 의미한다.이러한 POJO에 애플리케이션의 핵심 로직과 기능을 담아 설계하고 개발하는 방법을 POJO 프로그래밍이라고 한다.

POJO라는 용어는 이후에 주로 특정 [자바](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4)) 모델이나 기능, [프레임워크](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC) 등을 따르지 않은 자바 오브젝트를 지칭하는 말로 사용되었다. [스프링 프레임워크](https://ko.wikipedia.org/wiki/%EC%8A%A4%ED%94%84%EB%A7%81_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC)는 POJO 방식의 프레임워크이다.

- POJO는 Java EE를 사용하면서 해당 플랫폼에 종속되어 있는 무거운 객체들을 만드는 것에 반발하여 나타난 용어이다.
- 별도의 프레임 워크 없이 Java EE를 사용할 때에 비해 인터페이스를 직접 구현하거나 상속받을 필요가 없어 기존 라이브러리를 지원하기 용이하고, 객체가 가볍다.
- 즉, getter/setter를 가진 단순한 자바 오브젝트를 말한다.

### ApplicationContext

ApplicationContext는 인터페이스고 다양한 구현 클래스가 기본으로 제공된다. 사용 목적과 설정 파일 형식에 맞는 구현 클래스들을 선택해서 사용하면 된다. ApplicationContext 는 spring-beans 모듈의 o.s.beans.factory에 포함된 BeanFactory 인터페이스를 상속한다. 스프링 프레임워크의 스프링 빈 컨테이너 기능은 BeanFactory 인터페이스에 정의되어 있다. 그러므로 ApplicationContext도 스프링 빈 컨테이너의 기능을 제공한다. ApplicationContext는 BeanFactory 말고도 여러 가지 인터페이스를 상속한다. 그래서 스프링 빈 컨테이너 기능 외에 다른 기능을 제공한다.

- BeanFactory가 스프링 컨테이너의 최상위 인터페이스지만 ApplicationContext가 BeanFactory의 모든 기능을 가지고 있기 때문에 BeanFactory 를 사용하지 않고 ApplicationContext를 사용한다.
- ApplicationContext는 BeanFactory 말고 여러 가지 인터페이스를 생성한다.
    
    ⇒ 최상위 인터페이스 BeanFactory인 스프링 빈 컨테이너 기능 외에 다른 기능 제공
    
    ⇒ 다양한 기능을 가진 ApplicationContext를 기본 스프링 빈 컨테이너로 사용한다.
    

ApplicationContext가 관리하는 것들은 @Service @Component

ex. `import org.springframework.stereotype.Service;`

### 영속성 컨텍스트(Persistence Context)

- **엔티티를 영구 저장하고 관리하는 환경**으로, 엔터티 객체의 생명주기(life cycle)를 관리하는 컨텍스트 객체다. 스프링 프레임워크의 스프링 빈을 관리하는 ApplicationContext처럼 영속성 컨텍스트도 엔터티 객체를 관리한다.
- 서비스별로 하나의 **EntityManager Factory**가 존재하며 Entity Manager Factory에서 DB에 접근하는 트랜잭션이 생길 때 마다 쓰레드 별로 **EntityManager**를 생성하여 영속성 컨텍스트에 접근한다.
- 영속성 컨텍스트는 EntityManager를 생성할 때 만들어지며 EntityManager를 통해 영속성 컨텍스트에 접근하고 관리한다.
- 영속성 컨텍스트는 DB와 애플리케이션 사이에 위치하고 있어 객체 지향 프로그래밍이 가능하도록 돕는다.

### **EntityManager**

- EntityManager는 영속성 컨텍스트 내에서 엔티티들을 관리하고 있다.
- EntityManager는 JPA에서 제공하는 인터페이스로 스프링 빈으로 등록되어 있어 Autowired로 사용할 수 있다.

```java
@Autowired
private EntityManager entityManager;
```

- EntityManager 클래스는 엔티티 객체를 영속성 컨텍스트로 조회하거나 저장하고 삭제하는 기능을 제공한다.

### 멀티 쓰레드 Multi thread

![멀티 쓰레드](/assets/img/posts/2024-08-28-8.png)

- 애플리케이션 코드를 하나하나 순차적으로 실행하는 것은 쓰레드, 쓰레드는 서블릿을 호출한다.
- 자바 메인 메서드를 처음 실행하면 main이라는 이름의 쓰레드가 실행
- 쓰레드가 없다면 자바 애플리케이션 실행이 불가능
- 쓰레드는 한번에 하나의 코드 라인만 수행
- 동시 처리가 필요하면 쓰레드를 추가로 생성

![단일 쓰레드](/assets/img/posts/2024-08-28-9.png)

![쓰레드에서 한 요청의 처리가 지연되면 다음 요청 발생시 타임아웃 등 오류 발생](/assets/img/posts/2024-08-28-10.png)

![요청마다 쓰레드 생성](/assets/img/posts/2024-08-28-11.png)

**장점**

- 동시 요청을 처리할 수 있다.
- 리소스(CPU, 메모리)가 허용할 때 까지 처리가능
- 하나의 쓰레드가 지연 되어도, 나머지 쓰레드는 정상 동작한다.

**단점**

- 쓰레드는 생성 비용은 매우 비싸다.
    - 고객의 요청이 올 때 마다 쓰레드를 생성하면, 응답 속도가 늦어진다.
- 쓰레드는 컨텍스트 스위칭 비용이 발생한다.(실행시 동시 실행이 아니라 하나 실행하고 다음 실행하는 방식)
- 쓰레드 생성에 제한이 없다.
    - 고객 요청이 너무 많이 오면, CPU, 메모리 임계점을 넘어서 서버가 죽을 수 있다.

![쓰레드를 만들어놓고 풀에서 꺼내 쓰고 응답이 완료되면 반납](/assets/img/posts/2024-08-28-12.png)

**특징**

- 필요한 쓰레드를 쓰레드 풀에 보관하고 관리한다.
- 쓰레드 풀에 생성 가능한 쓰레드의 최대치를 관리한다. 톰캣은 최대 200개 기본 설정 (변경 가능)

**사용**

- 쓰레드가 필요하면, 이미 생성되어 있는 쓰레드를 쓰레드 풀에서 꺼내서 사용한다.
- 사용을 종료하면 쓰레드 풀에 해당 쓰레드를 반납한다.
- 최대 쓰레드가 모두 사용중이어서 쓰레드 풀에 쓰레드가 없으면?
    - 기다리는 요청은 거절하거나 특정 숫자만큼만 대기하도록 설정할 수 있다.

**장점**

- 쓰레드가 미리 생성되어 있으므로, 쓰레드를 생성하고 종료하는 비용(GPU)이 절약되고, 응답 시간이 빠르다.
- 생성 가능한 쓰레드의 최대치가 있으므로 너무 많은 요청이 들어와도 기존 요청은 안전하게 처리할 수 있다.

**WAS의 멀티 쓰레드 지원**

- 멀티 쓰레드에 대한 부분은 WAS가 처리
- 개발자가 멀티 쓰레드 관련 코드를 신경쓰지 않아도 됨
- 개발자는 마치 싱글 쓰레드 프로그래밍을 하듯이 편리하게 소스 코드를 개발
- 멀티 쓰레드 환경이므로 싱글톤 객체(서블릿, 스프링 빈)는 주의해서 사용