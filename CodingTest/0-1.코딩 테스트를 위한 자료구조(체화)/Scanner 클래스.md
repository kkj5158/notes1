# A1 . 주로하는 실수 , next() 와 nextLine() 의 차이점

next는 white space를 만나면 종료 되므로 뛰어쓰기가 포함되지 않은 하나의 단어를 받을때 사용하며. nextLine() 은 개행문자(Enter)를 만나면 종료 되므로 next()와 달리 문자열 안에 띄어쓰기를 할 수 있음 (공백을 포함할 수 있음)

# A2. 개행문자 비우기 

- 보통 nextLine() 메서드와 next 메서드를 혼용하여 사용할때 발생한다. 개행문자를 제대로 처리하지 않으면 예상치 못한 동작이 발생할 가능성이 크다. 

## 1. `nextInt()`, `nextDouble()` 등과 `nextLine()`을 혼용하는 경우

### 문제 발생 원인:

- `nextInt()`, `nextDouble()`, `next()` 등의 메서드는 숫자나 단어를 입력받은 후, 개행 문자(`\n`)는 소비하지 않고 입력 버퍼에 남깁니다.
    
- 이후 `nextLine()`을 호출하면 입력 버퍼에 남아 있던 개행 문자(`\n`)를 즉시 읽고 종료되므로, 실제 입력을 받을 기회를 잃어버립니다.
    

### 예제 코드 (문제 발생)

```java
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("나이를 입력하세요: ");
        int age = scanner.nextInt();  // 숫자 입력 후 개행 문자(\n)가 남음

        System.out.print("이름을 입력하세요: ");
        String name = scanner.nextLine();  // 개행 문자를 바로 읽고 종료됨

        System.out.println("나이: " + age);
        System.out.println("이름: " + name);
        
        scanner.close();
    }
}

```

### 실행 예시 (잘못된 동작)

makefile

```java
나이를 입력하세요: 25
이름을 입력하세요: 나이: 25
이름: 

```

- `nextInt()`는 `25`를 읽고, 개행 문자는 그대로 남김.
    
- `nextLine()`이 남아있던 `\n`을 읽고 바로 종료되어 `name`이 빈 문자열이 됨.

## 2. 해결 방법: `nextLine()`을 사용하여 개행 문자 제거

위 문제를 해결하려면 `nextInt()`, `nextDouble()` 등의 입력 후, **추가적으로 `scanner.nextLine()`을 한 번 호출하여 개행 문자를 소비**하면 됩니다.

### 수정된 코드 (올바른 동작)

```java
import java.util.Scanner;

public class ScannerExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("나이를 입력하세요: ");
        int age = scanner.nextInt();
        scanner.nextLine();  // 남아있는 개행 문자를 제거

        System.out.print("이름을 입력하세요: ");
        String name = scanner.nextLine();  // 정상적으로 문자열 입력 가능

        System.out.println("나이: " + age);
        System.out.println("이름: " + name);
        
        scanner.close();
    }
}

```

### 실행 예시 (올바른 동작)


```java
나이를 입력하세요: 25
이름을 입력하세요: 홍길동
나이: 25
이름: 홍길동

```

- `nextInt()`가 `25`를 읽음.
    
- `nextLine()`을 추가로 호출하여 `\n`을 제거.
    
- 이후 `nextLine()`이 정상적으로 사용자 입력을 받을 수 있음.

## 결론

**개행 문자를 비워야 하는 경우**

1. `nextInt()`, `nextDouble()` 등 숫자 입력 후 `nextLine()`을 사용할 때 → `scanner.nextLine()` 한 번 호출하여 `\n` 제거.
    
2. `next()` 후 `nextLine()`을 사용할 때 → `scanner.nextLine()`으로 개행 제거.
    
3. `while` 루프에서 `nextLine()`을 사용할 때 → 루프 전에 `scanner.nextLine()`을 호출하여 개행 제거.
    

개행 문자 문제를 방지하려면 **`nextLine()`만을 사용하거나, `next()` 계열과 `nextLine()`을 함께 사용할 때 개행 처리를 신경 써야 합니다.**