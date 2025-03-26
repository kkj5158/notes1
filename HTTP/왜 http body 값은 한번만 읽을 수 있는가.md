#http 
### 참고자료
[request body 한번만 읽어올수 있는 제약](https://yangbongsoo.tistory.com/28)
[Controller에서 HttpRequest Body 값은 왜 비워져 있을까?](https://velog.io/@saint6839/Controller%EC%97%90%EC%84%9C-HttpRequest-Body-%EA%B0%92%EC%9D%80-%EC%99%9C-%EB%B9%84%EC%9B%8C%EC%A0%B8-%EC%9E%88%EC%9D%84%EA%B9%8C)
[Spring은 Http Message Body를 어떻게 Java의 객체로 역/직렬화할까?](https://velog.io/@prayme/Spring%EC%9D%80-Http-Message-Body%EB%A5%BC-%EC%96%B4%EB%96%BB%EA%B2%8C-Java%EC%9D%98-%EA%B0%9D%EC%B2%B4%EB%A1%9C-%EC%97%AD%EC%A7%81%EB%A0%AC%ED%99%94%ED%95%A0%EA%B9%8C)
# Http body 의 특성

## http 프로토콜이 스트림 방식이여서 읽고 나면 데이터가 흘러가버린다.

복잡한 이유는 존재하지 않는다. HTTP 프로토콜은 요청과 응답을 전송하기 위해서 데이터를 스트림으로 전송하는데, 이러한 스트림은 일반적으로 한번만 읽을 수 있기 때문이다. 


그러므로, [[Servlet]] 과 [[SpringMVC]] 는 이러한 HTTP 프로토콜의 특성에 따라 구현되었기 때문에 HTTP 요청의 body 값을 한 번만 읽을 수 있다. body를 읽고 나면 해당 데이터는 메모리에서 삭제되거나 스트림에서 소비되므로 다시 읽을 수 없다. 

따라서 ,  만약 http 요청의 바디를 여러 번 읽고 싶다면 , 해당 바디 데이터를 메모리에 캐시하거나 별도의  저장소에 저장하여 여러 번 접근할 수 있도록 처리해야 한다. 

## 그러면 http 헤더는 ? 

헤더의 경우에는 http 요청 및 응답을 처리하는 방식이 바디 데이터와 다르다. 헤더는 여러 번 읽을 수 있고, 수정할 수도 있다. 

# Spring은 언제 http body를 객체로 변환할까? 

위의 내용을 숙지하게 되면, Spring이 언제 http body를 객체로 변환하게 되는지에 대한 의문이 들 수 밖에 없다. 

# Spring은 http body를 캐시로 변환해두는가? 