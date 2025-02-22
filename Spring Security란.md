#Spring #SpringSecurity #MVC 
##### 참고자료
[스프링 시큐리티 기본 API및 Filter 이해](https://catsbi.oopy.io/c0a4f395-24b2-44e5-8eeb-275d19e2a536)

# Spring Security란 

스프링 시큐리티는 스프링 기반 웹 애플리케이션의 인증과 권한을 담당하는 스프링의 하위 프레임워크이다. 여기서 인증(authenticate)은 로그인과 같은 사용자의 신원을 확인하는 프로세스를, 권한(authorize)은 인증된 사용자가 어떤 일을 할 수 있는지(어떤 접근 권한이 있는지) 관리하는 것을 의미한다.

# 도입과정

## 프로젝트 구성 및 의존성 추가

### dependency 추가
```maven
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

```gradle
implementation 'org.springframework.boot:spring-boot-starter-security'
```
### 스프링 시큐리티의 의존성 추가 시 일어나는 일들

- 서버가 기동되면 스프링 시큐리티의 초기화 작업 및 보안 설정이 이뤄진다.

- 별도의 설정이나 구현을 하지 않아도 기본적인 웹 보안 기능이 현재 시스템에 연동

	1.모든 요청은 인증이 되어야 자원에 접근이 가능하다.

	2.인증 방식은 폼 로그인 방식과 httpBasic로그인 방식을 제공한다.

	3.기본 로그인 페이지 제공

	![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fcfcc26bf-f580-4ad6-87a5-9b107c301e62%2Floginpage.png&blockId=f3ef150f-14f6-4c66-a675-827dd5999c19)

4.기본 계정 한 개 제공 user/랜덤문자열

![](https://oopy.lazyrockets.com/api/v2/notion/image?src=https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fa463a526-6230-4e83-8da8-b3b6aa52e992%2Fdefault_password.png&blockId=8804878d-3c36-46d4-bb14-c1d4a3eec0dc)



### 문제점

- 계정 추가, 권한 추가, DB 연동 등
- 기본적인 보안 기능 외에 시스템에서 필요로 하는 더 세부적이고 추가적인 보안기능 필요.