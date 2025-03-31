# 설명
 **java.util.Scanner**
- 파일, 입력 스트림 등에서 데이터를 읽어 구분자로 토큰화하고 다양한 타입으로 형변화하여 리턴해주는 클래스 
- 다음과 같은 방법으로 파일, 문자열 등 다양한 데이터를 읽어들일 수 있어 편리하다. 
	- Scanner(File source)
	- Scanner(InputStream source)
	- Scanner(String source)
- 입력 스트림을 다루는 방법을 몰라도 손쉽게 입력처리  가능 
- 데이터 형변환으로 인한 편리함 
- 대량의 처리시 수행시간이 비효율적이다.(느리다.)



# 주요 메서드

|              |                                                                                                |
| ------------ | ---------------------------------------------------------------------------------------------- |
| 메서드 명        | 특징                                                                                             |
| nextInt()    | - int 타입 반환  <br>- white space를 만나면 종료                                                         |
| nextDouble() | - double 타입 반환  <br>- white space를 만나면 종료                                                      |
| next()       | - String 타입 반환  <br>- white space를 만나면 종료                                                      |
| nextLine()   | - String 타입 반환  <br>- 개행문자(Enter)를 만나면 종료  <br>- next()와 달리 문자열 안에 띄어쓰기를 할 수 있음 (공백을 포함할 수 있음) |

# 체화해두기
- char를 받지 않는다 -> String으로 받아서 .tochar() 함수 사용하자 
- 