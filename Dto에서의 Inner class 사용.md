#MVC 
# Ineer Class 란?


중첩 클래스. 즉 클래스 내부에서 클래스를 선언하여서 사용하는 구조 . 
내부 클래스는 보통 static을 붙여서 다음과 같이 선언한다. 

```java
public class User{
	static class admin{
	}
}
```


# 너무 많은 dto를 내부 클래스로 선언해버리자.

예를 들어서 유저와 관련된 dto가 로그인, 회원가입 .. 기타 3~4개가 된다면 다음과 같이 유저 dto 클래스를 만들고 이를 묶어버리는 것이다. 

```java
public class UserDto{

	@Getter
	@Builder
	@AllArgsConstructor
	@NoArgsConstructor
	public static class UserJoinRequestDTO {
	    private String name;
	}

	@Getter
	@Builder
	@AllArgsConstructor
	public static class UserJoinResponseDTO {
	    private Long id;
	    private String name;
	}
}
```

# Json 안의 Json 구조를 해결하자 

	참고자료 
	https://velog.io/@chlwogur2/%EC%A4%91%EC%B2%A9%EB%90%9C-JSON%EC%9D%84-Java-Object-%EB%A1%9C-%EB%A7%A4%ED%95%91%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95-With-Jackson

