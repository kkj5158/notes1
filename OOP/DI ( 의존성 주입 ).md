#oop

### 참고자료
[Spring Core(2): 의존성 주입(DI), 개념, 방법, 장단점, 생성자 주입을 사용하자!](https://engineerinsight.tistory.com/46)
[Spring DI 스프링 의존성 주입 3가지 방법](https://cheershennah.tistory.com/227)
[다양한 의존성 주입 방법과 생성자 주입을 사용해야 하는 이유](https://mangkyu.tistory.com/125)

# 의존성이란 무엇인가 ?

시스템은 보통 하나의 객체로만 이루어지지 않는다. 시스템은 다양한 객체의 협력으로 구성되어있다. 이때 시스템 하나하나를 이루는 객체들의 연결을 의존성이라고 말할 수 있다. ==객체가 협력한다는 것은 서로 의존한다는 것이다.== 협력은 의존을 필요로 한다. 

# 스프링과 의존성
### 그놈의 DI와 IOC는 대체 무엇인가. 

스프링은 시스템상에서의 객체들의 협력관계(의존성 관계)를 DI(의존성 주입) IOC(제어의 역전)의 개념으로 객체지향적으로 풀어나간다. 협력관계는 개발자가 주입하지 않는다. (일일히 만들어서 직접 연결하지 않는다) 그것이 스프링에서 DI 컨테이너의 역할이다. 스프링은 의존성을 맺는 객체들이 협력관계를 맺고 체계적으로 복잡한 일을 처리하도록 자동 구성해준다. 

즉, 스프링에서의 DI란 개발자가 스프링컨테이너의 제어의 주도권을 넘긴채로 실행되는것이다. 이는 개발자의 일을 줄여주므로 명확한 장점을 가진다. 그렇다면 단점으로는 어떠한 것들이 있을까 ? 

# 의존성 주입과 단점

## 자동으로 해주니, 잘 알지는 못하는데요...;;

스프링의 자동 의존성 주입의 뒷배경을 명확히 알고 있는 사람이라면 ( 스프링은 객체지향의 5대원칙을 준수하기 위해서 의존성 주입이라는 방법을 택한다.) 의존성 주입은 막강한 장점을 가진다. 하지만 의존성 주입을 단순히 Autowire 수준으로만 이해하고 있는 개발자라면. 자신이 개발하는 객체들이 어떤 의존성을 가지는지. 즉 어떤 협력구조로 가지고 전체적인 일들을 해나가는지 놓칠 가능성이 높다. ==즉 자동으로 해주다보니. 개발자 스스로가 전체적인 시스템을 보는 눈을 놓칠 가능성이 높다는 의미이다.== 

그러므로, 개발자는 의존성 주입과 스프링 컨테이너의 역할을 명확히 이해하고. 스프링을 사용해야한다. 자신이 지금 개발하고 있는 애플리케이션이 어떤 협력구조를 가지고 있는지 언제나 파악하고 이를 사용해야한다. ==그렇다면 의존성 주입은 굉장히 막강한 객체지향 프레임워크 철학이 될것이다.==

# 의존성을 주입하는 방법

## 생성자 주입 

클래스의 생성자에 @Autowired를 붙여서 주입 


```java
@Controller public class Controller{    
private Service service;    

@Autowired    
public Controller(Service service){      
this.service = service;    

} 

}
```
## 필드 주입

흔히 가장 많이 사용하는 방법. 필드에 Autowired 사용 
```java
@Controller public class Controller{   
@Autowired  private Service service; 
}
```

### 수정자 주입

Setter 혹은 사용자 정의 메서드를 통해 의존관계 주입 . 

```java
@Controller public class Controller{    
private Service service;    
@Autowired public setService(Service service){      
this.service = service;    
} }
```

스프링 팀에서는 생성자 주입을 권장한다. 

# 생성자 주입 권장의 이유

## 객체의 불변성 확보 

실제로 개발을 하다 보면  의존 관계의 변경이 필요한 상황은 거의 없다. 하지만 수정자 주입이나 일반 메소드 주입을 이용하면 불필요하게 수정의 가능성을 열어두어 유지보수성을 떨어뜨린다. 그러므로 생성자 주입을 통해서 변경의 가능성을 배제하고 불변성을 보장하는 것이 좋다. 

## 테스트 용이

테스트가 특정 프레임워크에 의존하는 것은 침투적이므로 좋지 못하다. 그러므로 가능한 순수 자바로 테스트를 작성하는 것이 가장 좋은데, 생성자 주입이 아닌 다른 주입으로 작성된 코드는 순수한 자바 코드로 단위 테스트를 작성하는 것이 어렵다. 

## 순환참조 에러 방지 

생성자 주입을 사용하면 애플리케이션 구동 시점 (객체의 생성 시점) 에 순환 참조 에러를 예방할 수 있다. 예를 들어 다음과 같이 필드를 서로 호출하는 코드가 있다고 하자. 

##  ==final 키워드 작성 및 Lombok과의 결합== 

생성자 주입을 사용하면 필드 객체에 final 키워드를 사용할 수 있으며, 컴파일 시점에 누락된 의존성을 확인할 수 있다. 반면에 다른 주입 방법들은 객체의 생성(생성자 호출) 이후에 호출되므로 final 키워드를 사용할 수 없다.

또한 final 키워드를 붙이면 Lombok과 결합되어 코드를 간결하게 작성할 수 있다. Lombok에는 final 변수를 위한 생성자를 대신 생성해주는 @RequiredArgsConstructor를 [여기](https://mangkyu.tistory.com/78) 에서 살펴보았다. Spring과 같은 DI 프레임워크는 Lombok과 환상적인 궁합을 보여주는데, 위에서 작성했던 생성자 주입 코드를 Lombok과 결합시키면 다음과 같이 간편하게 작성할 수 있다.


```java
@Service
@RequiredArgsConstructor
public class UserService {

    private final UserRepository userRepository;
    private final MemberService memberService;

    public void register(String name) {
        userRepository.add(name);
    }

}


```

