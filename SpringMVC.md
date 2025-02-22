#MVC 
### 참고자료
<자바 , 웹을 다루는 기술 21장 > 스프링 MVC 
[스프링 MVC - 구조  이해](https://blogshine.tistory.com/261) 

# 배경지식
[[MVC 패턴]]

# Spring MVC
스프링 프레임워크는 웹 애플리케이션 개발에 필요한 여러가지 기능을 미리 만들어서 제공한다. MVC 기능도 그 중 하나이다. 스프링에서 제공하는 기능 사용법을 익히고 나면 MVC 기능을 일일이 만들 필요 없이 편리하게 MVC 기능을 사용할 수 있다. 

다음은 스프링에서 지원하는 MVC 기능의 특징이다.

## Spring MVC 기능 
- 모델 2 아키텍쳐를 지원한다. [[MVC Model 1 vs MVC Model2]]
- 스프링과 다른 모듈과의 연계가 쉽다. 
- JSP , 타임리프와 같은 View 기술과의 연계가 쉽다. ( 스프링에서는 타임리프를 기본 뷰 템플릿으로 지원한다.)

## Spring MVC의 구조

![[스프링 mvc구조.png]]

## 수행 과정 

 _일반적으로 spring mvc에서의 핸들러는 컨트롤러를 말한다. 그러므로 여기에서는 핸들러를 컨트롤러로 칭하겠다._ 

1. DispatcherServlet이 모든 웹 브라우저로부터의 요청을 받는다.
2. 컨트롤러 조회 : 컨트롤러 매핑을 통해서 URL에 매핑된 컨트롤러(핸들러)를 조회한다.
3. 컨트롤러 어댑터 조회 및 실행 : 컨트롤러를 실행할 수 있는 컨트롤러 어댑터를 조회한다. 해당 어댑터는 컨트롤러를 호출한다. 
4. 컨트롤러 실행 : 호출된 컨트롤러가 실행된다. 
5. 컨트롤러 어댑터는 컨트롤러가 반환하는 정보를 ModelandView로 반환한다. 
6. ViewResolver는 호출을 받고, 요청된 View를 반환한다. 
7. View의 처리 결과를 DispatcherServlet으로 보냅니다. 
8. DispathcerServlet은 model을 렌더링 하여서 최종 결과를 브라우저로 전송합니다. 


## 구성요소들 

### DispatcherServlet

스프링 MVC는 프론트 컨트롤러 패턴으로 구현되어 있다. MVC의 프론트 컨트롤러가 바로 DispatcherServlet이다. 해당 DispatcheServlet도 부모 클래스에서 HttpServlet을 상속 받아서 사용하고, 서블릿을 동작한다. [[Servlet]]

![[dispatcher서블릿.png]]

