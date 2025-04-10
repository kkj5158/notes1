# Kafka란 무엇인가
#Architecture
#### 참고문서
[링크드인과 카프카 탄생배경](https://log-laboratory.tistory.com/143)

## 카프카의 탄생 배경

### 데이터를 보내고 받는다. 하지만, 이게 너무 많다면..?
### 끝도 없이 많아지는 데이터 파이프라인
소셜 네트워크 사이트인 '링크드인'에서는 파편화된 데이터 수집 분배 아키텍쳐를 운영하는데에 큰 어려움을 겪는다. 

데이터의 수집과 분배라 하면, 데이터를 생성하는 소스 애플리케이션과 해당 데이터가 도착하는 (최종 적재되는) 타깃 애플리케이션의 존재를 염두에 둬야 한다. 

링크드인에서는 초기 운영시에 , 단방향 통신을 통해 소스 애플리케이션에서 타깃 애플리케이션으로 연동하는 소스코드를 작성했고 아키텍쳐가 복잡하지 않았으므로 운영이 힘들지 않았다. 그러나 서비스가 거대해짐에 따라 다음과 같이, 데이터의 출발지와 도착지를 한눈에 파악할 수 없는 구조가 되어버린다. 

![[링크드인_카프카구조.png]]

소스 애플리케이션과 타킷 애플리케이션을 연결하는 파이프라인 개수가 많아지면서 소스코드 및 버전 관리에서 이슈가 생겼다. 그리고 타깃 애플리케이션에 장애가 생길 경우 그 영향이 소스 애플리케이션에 그대로 전달되었다. 
(도착지가 받을 준비가 되어있지 않으면 데이터를 보내는 소스애플리케이션도 데이터를 보낼 수 없다. (데이터의 유실문제))

위의 아키텍쳐 처럼 엔드투엔드(End to End)연결 방식의 아키텍처는 많은 문제점이 있다.

### End to End 방식의 문제점 

#### 1.시스템의 복잡도 증가 
실시간 트랜잭션 처리와 비동기 처리가 동시에 이뤄지지만 통합된 전송 영역이 없으니 복잡도가 증가한다. 복잡도가 증가하므로 문제가 발생했을때 , 조치를 취하려면 여러 시스템을 동시에 점검해야한다. 
#### 2. 데이터 파이프라인 관리의 어려움 

##### 수많은 데이터 파이프라인을 통하는 데이터들의 포맷은 ?? -> 당연히 일관될 수 없다. 
실시간 트랜잭션 데이터 베이스, 아파치 하둡, 모니터링 시스템, 키-값 저장소 등 많은 데이터 시스템들이 있는데, 이 시스템에 저장된 동일한 데이터를 개발자나 개발 부서는 각기 다른 방법으로 파이프 라인을 만들고, 유지하게 되어 있다. 하지만 데이터 파이프라인들은 통합 데이터 분석을 위해 필연적으로 서로 연결되어야 한다면, 각 파이프라인별로 데이터 포맷과 처리하는 방법들이 완전히 달라서 데이터 파이프라인은 확장하기 어려웠고, 조정하고 운영하는 것은 엄청난 노력이 필요하다.

## 해결 방법의 모색 -> Kafka의 탄생 

해당 문제점들을 해결하기 위해서 만들어진 것이 바로 Kafka이다. Kafka는 다음의 특징을 만족하면서 해당 문제점들을 해결한다. 

### Kafka의 특징 

#### 1. 프로듀서와 컨슈머의 분리 
#### 2. 메시지 시스템과 같이 영구 메시지 데이터를 여러 컨슈머에게 허용 
#### 3. 높은 처리량을 위한 메시지 최적화 
#### 4. 데이터가 증가함에 따라 스케일 아웃이 가능한 시스템 


![[링크드인_카프카_개선.png]]

다음과 같이 사내에서 발생는 모든 이벤트/데이터의 흐름을 중앙에서 관리하는 카프카를 적용한 결과, 서비스 아키텍쳐가 예전과 비교할 수 없을 정도로 매우 깔끔해졌다. 

### Kafka의 장점

#### 1. 서비스 아키텍쳐의 깔끔함 . 
#### 2. 개발자는 카프카에 데이터를 적재하기만 하면 된다. 
- 만약 , 데이터를 생성하는 소스애플리케이션 개발자라면 카프카의 도입 이전에는 
	- 1. 어느 목적지 애플리케이션에 데이터를
	- 2. 어떤 형식에 맞춰서 보내야하는지
	- 3. 복잡한 아키텍쳐구조와 연관도를 모두 파악하여서 
- 개발 해야만 했다. 
- 하지만, 카프카 개발 이후에는 개발자는 카프카에 데이터를 적재하기만 하면 된다. 
	- 이는 계층 분리에 따라서 개발자가 자신의 본연에 업무에 더욱 집중하면 된다는 의미이다. ! 

