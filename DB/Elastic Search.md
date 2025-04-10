#elasticSearch #DB #nosql

# 엘라스틱 서치 
## 엘라스틱 서치란 ? 
### 루씬(자바 라이브러리) 기반의 오픈소스 검색 엔진 . 
### 준 실시간 검색 시스템 
	실시간이라고 생각될만큼 색인된 데이터가 빠르게 검색됩니다. 
### 고가용성을 위한 클러스터 구성
	한 대 이상의 노드로 클러스터를 구성하여 높은 수준의 안정성을 달성하고 부하 분산이 가능합니다. 
### 동적 스키마 생성
	입력될 데이터들에 대해 미리 스키마를 정의하지 않아도 동적으로 스키마 생성이 가능합니다. 
### Rest API 기반의 인터페이스
	Rest API 기반의 인터페이스를 제공하여서 비교적 사용을 위한 진입장벽이 낮다. 

## 클러스터 
컴퓨터 클러스터는 여러대의 컴퓨터들이 연결되어 하나의 시스템처럼 동작하는 컴퓨터들의 집합을 말한다. Elasic search도 여러대의 노드들이 **각자의 역할**을 바탕으로 연결되어서 하나의 시스템처럼 동작하게 되어있다. 
![[엘라스틱서치_클러스터구성.webp]]
클러스터의 성능이 부족하면 노드를 늘려서 대응할 수 있다. 


### 노드의 종류 

#### 마스터노드 
	클러스터 상태 관리 및 메타데이터 관리 
#### 데이터 노드
	문서 색인 및 검색 요청 처리
#### 코디네이팅 노드 
	검색 요청 처리
#### 인제스트 노드
	색인되는 문서의 전처리 

### 마스터 노드와 마스터 후보 노드 

#### 마스터 노드 
	지금 클러스터에서 마스터노드의 역할을 하고 있는 노드 
#### 마스터 후보 노드 
	 마스터 노드에서 문제가 생겼을때 , 마스터 노드가 될 수 있는 노드 
마스터 노드가 죽으면 마스터 후보 노드들 중에서 새로운 마스터 노드가 생긴다. 

### 여러개의 노드 , 하나의 시스템 동작

**어떤 노드에 어떤 요청을 해도 동일한 응답을 준다.**

> 고객센터를 생각해보자. 다양한 업무를 여러 상담사들이 각자 업무에 따라 분담하지만, 어떤 상담사에게 요청을 해도 결국 담당상담자에게 문의가 들어간다. 엘라스틱서치도 이와 같이 어떤 노드에 어떤 요청을 해도 동일한 응답을 준다. 

그럼에도 , 각각의 노드가 본인의 역할에 충실할 수 있도록 구성하는것이 중요합니다. 

> 대부분의 상담센터는 ARS의 번호를 통해서 각각의 업무에 해당하는 상담사를 바로 연결할 수 있도록 설계되어있습니다. 이와 같이 엘라스틱 서치도 앞단에 로드밸런서를 두고 요청을 각각의 역할에 따라 노드에 분할 할당합니다. 


## 인덱스와 샤드 

### 인덱스 
![[엘라스틱서치와 RDBMS의 관계.png]]
RDBMS의 데이터베이스 개념, 문서가 저장되는 논리적인 공간 
**인덱스를 설계하는 것이 Elastic Search를 사용하기 위해 고려해야 하는 첫 단계입니다.**

만약 도서관 자료 검색시스템을 만든다고 가정한다면 , 
![[인덱스 설계.png]]

인덱스 설계에 따라 달라지는 문서의 구조및 검색 쿼리 

![[인덱스 설계의 장단점.png]]

하나의 인덱스로 단순하게 시작해서, 사용 패턴에 따라 인덱스를 별도로 운영하는 식으로 진행하는것이 좋다. 

### 샤드 

인덱스 안에서 문서가 저장되는 단위 . 
하나의 인덱스는 반드시 하나 이상의 샤드를 가집니다. 

#### 종류

![[샤드의종류.png]]

#### 샤드 라우팅 

라우팅은 문서가 저장되는 순서를 의미한다. 그래서 , 샤드의 개수가 바뀐다면 문서가 저장되는 규칙이 완전히 바뀌게 된다. 

## 검색 과정 이해하기 

![[엘라스틱서치 검색과정.png]]

### Inverted Index 

문자열을 분석한 결과를 저장하고 있는 구조체. 

### Analyzer
![[에너라이저.png]]


