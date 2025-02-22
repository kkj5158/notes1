#MVC 
# JsonProperty 란 ? 

### 참고자료 
[ @JsonProperty 사용법에 대한 모든 것](https://stir.tistory.com/387)

## 정의 
@JsonProperty는 JSON 직렬화 시 설정할 수 있는 이름을 지정하는 어노테이션이다 . 

## 사용예시


# ISSUE

### 참고자료 
[@JsonProperty(required=true) doesn't work for 2.6.0-rc4](https://github.com/FasterXML/jackson-databind/issues/869)

## 2.6 이후 버전부터는 required=true validation default check 가 불가능하다. 

## DTO

### 다음의 dto 구조는 required=true 여도 , 필수값 체크를 해주지 않습니다. 
```java
@Getter  
@Setter  
public class CommonRequestDto {  

	@JsonProperty(value = "order_id", required = true)
    private String orderId;  
	@JsonProperty(value = "product_name", required = true)
    private String prductName;  
	@JsonProperty(value = "customer_num", required = true)
    private int customerNum;  
  

}
```

2.6 이전에는 다음의 dto구조가 있다면, json body 값에 <required = true> 로 지정되어 있는 필드 값이 안들어오면 Exception을 던져주었다. 하지만 2.6 버전 이상부터는 다음의 구조에서는 더 이상 Exceton을 던져주지 않는다. ==사실상 required = true 속성이 있으나 없으나 동일한 동작을 하게 되는것이다.== 
# 이전 버전처럼 사용하려면, 
### @JsonCreator를 생성자에 붙여줘야 한다. 

```java
@Getter  
@Setter  
public class CommonRequestDto {  
  
    private String orderId;  
  
    private String prductName;  
  
    private int customerNum;  
  
    @JsonCreator  
    public CommonRequestDto(  
        @JsonProperty(value = "order_id", required = true) String orderId,  
@JsonProperty(value = "product_name", required = true) String prductName,  
    @JsonProperty(value = "customer_num", required = true) int customerNum){  
        this.orderId = orderId;  
        this.prductName = prductName;  
        this.customerNum = customerNum;  
    }  
  
  
}
```


2.6 이상부터는 다음의 구조에서만 required = true 속성이 적용되고, required = true 필수 값이 들어오지 않는다면 Exception을 발생시킨다. 




