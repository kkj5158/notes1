#MVC 

### 참고자료
[@ControllerAdvice와 RequestBodyAdvice을 이용한 RequestBody 데이터 변경 방법](https://flambeeyoga.tistory.com/entry/ControllerAdvice%EC%99%80-RequestBodyAdvice)
[Request Body를 따로 읽고 싶을 때](https://stuffdrawers.tistory.com/10)
[RequestBodyAdvice in Spring Boot](https://medium.com/@truongbui95/requestbodyadvice-in-spring-boot-a8a40ea59e6d)
# @ControllerAdvice
[[@ControllerAdvice]]

RequestBodyAdvice를 이해하기전에 @ControllerAdvice에 대해서 먼저 알아보자. 
ControllerAdvice는 짧게 말해서, Spring이 제공하는 [[Spring AOP]]의 기능중에 하나이며, 전역에 있는 컨트롤러에 공통적으로 사용되는 것이 있을때 , 적용시켜주는 Annotation이다.  


# RequestBodyAdvice ? 

[RequestBodyAdvice](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/web/servlet/mvc/method/annotation/RequestBodyAdvice.html) 는 http 요청(request 요청)이 컨트롤러에서 Dto객체로 변환되기전에 전처리 작업을 할 수 있도록 스프링에서 제공하는 인터페이스이다. 해당 인터페이스 구현을 통해서 요청의 전처리 작업을 처리하는 클래스를 정의할 수 있다.  

## 미리 알아두어야할 http의 특성

[[InterCeptor]] 가 아니더라도 http의 body 값은 한번 읽히면 날아가버린다는 특성이 동일하다. [[왜 http body 값은 한번만 읽을 수 있는가]]

그러므로 RequestBodyAdvice에서도 http의 body값이 읽힌다면 http body 값은 스트림에서 비워지게 된다. 그러면 다음과 같은 의문이 들 수 있다. 


https://chat.openai.com/c/f47da008-30d8-48de-a8a2-eea85a5ac47c -> 정리해두기 

## 구현 함수

### supports 

RequestBodyAdvice의 처음과 끝에서 실행되며 , @ControllerAdvice 범위내에서 Controller가 실행이 될 때 , Controller 단에 대해서 체크하는 곳. 

### beforebodyread

Spring MVC가 RequestBody를 읽기전에 실행되는 Method 이다. 

### afterbodyread

Sprinng MVC가 RequestBody를 읽은 후에 실행되는 Method 이다.

### handleEmptyBody

RequestBody가 비어져 있을때 임의로 넣어줄 수 있는 곳. 

