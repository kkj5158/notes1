# StringBuilder 란?
## StringBuilder를 왜 사용해야 할까 

### String의 문제점 
자바에서 문자열을 생각하면 자연스럽게 String이 떠오른다. 

```java
String str1 = "Hello ";
String str2 = "Java";
str1 += str2;

System.out.println(str1); //"Hello Java"
```

이런 식으로 2개의 객체가 있을 때 , str1 + str2 와 같은 연산을 하게 되면 새로운 String을 생성하는 것을 알 수 있다. 

String은 소위 불변 객체라고 한다. 즉 String 객체는 한 번 생성되면 변경할 수 없다. 위와 같이 + 연산자를 사용하여 문자열을 연결하면  연결할 때마다 새로운 문자열 객체가 생성된다는 것을 의미한다. 또한 이전에 있던 문자열은 JVM의 GC가 처리하게 된다. 
따라서 , String 객체를 더하는 행위는 메모리 할당과 메모리 해체를 발생시키며 더하는 연산이 많아진다면 성능적으로 좋지 않다. 

### StringBuilder의 등장 

위와 같은 문제점을 해결하기 위해서 StringBuilder가 등장하게 되었다. StringBuilder는 String과 다르게 mutable한 성질을 가지고 있다. 즉 값이 변할 수 있다는 것이다. 
StringBuilder는 String과 문자열을 더할 때 새로운 객체를 생성하는 것이 아니라 기존의 데이터에 더하는 방식을 사용하기 때문에 속도도 빠르며 상대적으로 부하가 적다.

따라서 긴 문자열을 더하는 상황이 발생할 경우 StringBuffer 또는 StringBuilder를 적극적으로 사용해보자.

StringBuffer와 StringBuilder의 차이는 멀티스레드 환경에서 thread-safe 여부가 다르다. StringBuffer는 thread-safe 하므로 여러 쓰레드에서 동시에 해당 문자열에 접근한다면 사용을 고려하고, 그렇지 않다면 StringBuilder를 사용하는 것이 성능에 더 유리하다. (성능과 thread-safe는 반비례라고 생각하면 된다.)

정리하면

1. 문자열 변경이 빈번하지 않는다면 String 사용을 고려
2. 문자열이 빈번하게 변경되면서 멀티쓰레드 환경이라면 StringBuffer 사용을 고려
3. 문자열이 빈번하게 변경되면서 멀티쓰레드 환경이 아니라면 StringBuilder 사용을 고려

