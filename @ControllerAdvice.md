#MVC 
### 참고자료
[@ControllerAdvice와 RequestBodyAdvice을 이용한 RequestBody 데이터 변경 방법](https://flambeeyoga.tistory.com/entry/ControllerAdvice%EC%99%80-RequestBodyAdvice)

# @ControllerAdvice 란?

RequestBodyAdvice를 이해하기전에 @ControllerAdvice에 대해서 먼저 알아보자. 
ControllerAdvice는 짧게 말해서, Spring이 제공하는 [[Spring AOP]]의 기능중에 하나이며, 전역에 있는 컨트롤러에 공통적으로 사용되는 것이 있을때 , 적용시켜주는 Annotation이다.  

# 활용 
가장 많이 알려진 활용법은 전역 예외처리를 담당하는 Global ExceptionHandler를 만드는 방법일것이다. 그 외에도 다음과 같은 활용 방법이 존재한다. 

## Global ExceptionHandler 


## @ModelAttribute


## @InitBinder

## RequestBodyAdvice , ResponseBodyAdvice
