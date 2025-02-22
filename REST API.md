#http #API 

# REST [[API]]

## REST란 ?
Representational State Transfer의 약자로 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든것을 의미한다. 

1. HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고,
2. HTTP Method(POST, GET, PUT, DELETE, PATCH 등)를 통해
3. 해당 자원(URI)에 대한 CRUD Operation을 적용하는 것을 의미합니다.

## **REST 구성 요소**

1. **자원(Resource) : HTTP URI**
2. **자원에 대한 행위(Verb) : HTTP Method**
3. **자원에 대한 행위의 내용 (Representations) : HTTP Message Pay Load**

## REST API
**REST API란 REST의 원리를 따르는 API를 의미합니다.**

**1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.**

**2. 마지막에 슬래시 (/)를 포함하지 않는다.**

**3. 언더바 대신 하이폰을 사용한다.**

**4. 파일확장자는 URI에 포함하지 않는다.**

**5. 행위를 포함하지 않는다.**


## **RESTful이란?**

**RESTFUL이란 REST의 원리를 따르는 시스템을 의미합니다. 하지만 REST를 사용했다 하여 모두가 RESTful 한 것은 아닙니다.  REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful하다 말할 수 있으며

*모든 CRUD 기능을 POST로 처리 하는 API 혹은 URI 규칙을 올바르게 지키지 않은 API는* REST API의 설계 규칙을 올바르게 지키지 못한 시스템은 REST API를 사용하였지만 RESTful 하지 못한 시스템이라고 할 수 있습니다.

#### 참고자료
[[Network] REST란? REST API란? RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)

