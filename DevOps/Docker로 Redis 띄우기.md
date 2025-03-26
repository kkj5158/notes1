#DevOps 

Redis는 cache 용도로 널리 사용되는 NoSQL DB입니다. 기본적으로 인메모리 DB이기 떄문에 디스트 스토리지에 데이터가 보관되는 것이 아니라 컴퓨터 메모리에 보관됩니다. 즉, Redis는 데이터를 메모리에 저장하고 메모리에 있는 데이터를 조회합니다. 

오늘은 docker-compose로 Redis 컨테이너를 생성하고 실행하는 방법에 대해 살펴보겠습니다. 영속성을 보장할 수 있도록 docker-compose.yml을 작성하는 것이 생각보다 어려웠습니다. 영속성을 보장한다는 것은 docker-compose down으로 컨테이너를 정지시키고 삭제한 후에 다시 docker-compose up -d로 컨테이너를 생성하고 실행했을 때 이전에 저장했던 데이터가 남아있다는 뜻입니다. (제가 이해한 바로는 그렇습니다. 혹시 제 이해가 틀렸다면 꼭 알려주세요.)

## 1. Redis 도커 이미지 가져오기

일단 Redis 도커 이미지가 필요합니다. docker pull 명령어로 redis 최신 버전을 가져옵니다. 

```shell
docker pull redis
```

이미지를 잘 가져왔는지 확인하려면 docker images 명령어로 확인합니다. 

## 2. docker-compose.yml 작성

다음과 같이 docker-compose.yml 파일을 작성합니다.

```shell
# 파일 규격 버전
version: "3.1"

# 실행하려는 컨테이너들 정의
services:  
  # 서비스명
  redis_container:
    # 사용할 이미지
    image: redis:latest
    # 컨테이너명
    container_name: redis_test
    # 접근 포트 설정(컨테이너 외부:컨테이너 내부)
    ports:
      - 6379:6379
    # 스토리지 마운트(볼륨) 설정
    volumes:
      - ./redis/data:/data
      - ./redis/conf/redis.conf:/usr/local/conf/redis.conf
    # 컨테이너에 docker label을 이용해서 메타데이터 추가
    labels:
      - "name=redis"
      - "mode=standalone"
    # 컨테이너 종료시 재시작 여부 설정
    restart: always
    command: redis-server /usr/local/conf/redis.conf
```

## 3. docker-compose로 컨테이너 생성 및 실행

이제 docker-compose.yml이 존재하는 디렉토리에서 다음 명령어로 Redis 컨테이너를 생성하고 실행합니다. 

```
docker-compose up -d
```

잘 생성되고 실행되었는지 docker ps -a 명령으로 확인합니다. 

## 4. redis-cli로 데이터 입력, 조회 확인

이제 Redis가 잘 작동하는지 확인하기 위해 redis 컨테이너에 접속해서 redis-cli를 실행하겠습니다. 저의 경우는 컨테이너명을 redis_test라고 했기 때문에 다음과 같이 명령하면 컨테이너에 접속해서 redis-cli가 실행됩니다. 

```
docker exec -it redis_test redis-cli
```

데이터를 쓰고, 읽어보겠습니다. 

```
SET watermelon 15000 
GET watermelon
```

![](https://blog.kakaocdn.net/dn/cxXUDP/btrVzZlrb3z/hviv55zwZ7279MYO1zrmT0/img.png)

키 watermelon, 값 15000이란 데이터가 잘 삽입되었고, 키가 watermelon인 데이터를 잘 읽어냈습니다.


참고자료 
	https://bskyvision.com/entry/docker-docker-compose%EB%A1%9C-Redis-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88-%EC%8B%A4%ED%96%89%ED%95%98%EA%B8%B0
