#Docker #DevOps 

## [[Docker]]란 ?  
- 개발환경을 각각 격리시켜주는 격리 컨테이너.

# ELK의 구축

본격적으로 , ELK 프로젝트를 시작하기전에 ELK를 Docker와 Docker-Compose를 통해서 구축해보자. 
Docker라는 개념을 처음 접해보는 개발자라면 지금까지 개발환경들을 격리시키지 않고, 환경에 그대로 개발환경을 구축해왔을텐데. ELK를 Docker와 Docker-Compose를 통해서 구축하면 다음의 이점이 있다. 

## 왜 Docker & Docker-Compose를 사용하는가?

리눅스 기반 서버에 도커 설치는 다음 글을 참고하자 
[[Docker 와 Docker-Compose 를 이용한 서버 구축]]

#### 쉬운 배포 및 관리 

[[Docker-Compose]] 참고해보기 . 

Docker와 Docker-compose 스크립트가 한번 작성되면 , 이후에는 환경에 ELK 스택을 구축하는 일이 매우 쉰워진다. 각자 프로그램별로 세팅하고 싶은 설정값들도 스크립트 내에 기입이 가능하므로 일관적인 환경을 효율적으로 구축이 가능하다. 

보통 ELK 스택은 3가지의 컨테이너가 동시에 관리해야하는 경우가 많으므로 컨테이너를 동시에 관리할 수 있는 Docker-Compose를 사용할 것이다. 구글링을 하다보면 대표적으로 이용하는 ELK 세팅이 마쳐진 Docker-Compose yml 파일을 얻을 수 있다. 

https://github.com/deviantony/docker-elk

해당 레포지토리를 사용할것이다. 해당 레포지토리의 리드미를 따라가면서 작업을 진행해나간다. 


#### docker-compose yml 파일


```shell
version: '3.7'
services:
# 'setup' 서비스는 Elasticsearch 내부에 'logstash_internal' 및 'kibana_system'과 같은 사용자를
# 초기화하는 일회성 스크립트를 실행합니다. 이때 초기화는 '.env' 파일에 정의된 비밀번호 값을 사용합니다.
# 또한 일부 사용자에 필요한 역할도 생성합니다.
#
# 이 작업은 스택의 *초기* 시작 중에만 수행되어야 합니다. 이후 실행에서는 기존 사용자의 비밀번호가
# '.env' 파일에 정의된 값으로 재설정되며, 내장 역할은 기본 권한으로 복원됩니다.
#
# 기본적으로 'docker compose up'에 의해 시작되는 서비스에서 제외됩니다.
# 이는 해당 서비스가 비-default 프로필에 속하기 때문입니다.
# 실행하려면 Compose 명령에 '--profile=setup' CLI 플래그를 제공하거나,
# 'docker compose up setup'과 같이 서비스 이름을 사용하여 실행합니다.

  setup:
    profiles:
      - setup
    build:
      context: setup/
      args:
        ELASTIC_VERSION: ${ELASTIC_VERSION}
    init: true
    volumes:
      - ./setup/entrypoint.sh:/entrypoint.sh:ro,Z
      - ./setup/lib.sh:/lib.sh:ro,Z
      - ./setup/roles:/roles:ro,Z
    environment:
      ELASTIC_PASSWORD: ${ELASTIC_PASSWORD:-}
      LOGSTASH_INTERNAL_PASSWORD: ${LOGSTASH_INTERNAL_PASSWORD:-}
      KIBANA_SYSTEM_PASSWORD: ${KIBANA_SYSTEM_PASSWORD:-}
      METRICBEAT_INTERNAL_PASSWORD: ${METRICBEAT_INTERNAL_PASSWORD:-}
      FILEBEAT_INTERNAL_PASSWORD: ${FILEBEAT_INTERNAL_PASSWORD:-}
      HEARTBEAT_INTERNAL_PASSWORD: ${HEARTBEAT_INTERNAL_PASSWORD:-}
      MONITORING_INTERNAL_PASSWORD: ${MONITORING_INTERNAL_PASSWORD:-}
      BEATS_SYSTEM_PASSWORD: ${BEATS_SYSTEM_PASSWORD:-}
    networks:
      - elk
    depends_on:
      - elasticsearch
  elasticsearch:
    build:
      context: elasticsearch/
      args:
        ELASTIC_VERSION: ${ELASTIC_VERSION}
    volumes:
      - ./elasticsearch/config/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml:ro,Z
      - elasticsearch:/usr/share/elasticsearch/data:Z
    ports:
      - 9200:9200
      - 9300:9300
    environment:
      node.name: elasticsearch
      ES_JAVA_OPTS: -Xms512m -Xmx512m
      # Bootstrap password.
      # Used to initialize the keystore during the initial startup of
      # Elasticsearch. Ignored on subsequent runs.
      ELASTIC_PASSWORD: ${ELASTIC_PASSWORD:-}
      # Use single node discovery in order to disable production mode and avoid bootstrap checks.
      # see: https://www.elastic.co/guide/en/elasticsearch/reference/current/bootstrap-checks.html
      discovery.type: single-node
    networks:
      - elk
    restart: unless-stopped
  logstash:
    build:
      context: logstash/
      args:
        ELASTIC_VERSION: ${ELASTIC_VERSION}
    volumes:
      - ./logstash/config/logstash.yml:/usr/share/logstash/config/logstash.yml:ro,Z
      - ./logstash/pipeline:/usr/share/logstash/pipeline:ro,Z
    ports:
      - 5044:5044
      - 50000:50000/tcp
      - 50000:50000/udp
      - 9600:9600
    environment:
      LS_JAVA_OPTS: -Xms256m -Xmx256m
      LOGSTASH_INTERNAL_PASSWORD: ${LOGSTASH_INTERNAL_PASSWORD:-}
    networks:
      - elk
    depends_on:
      - elasticsearch
    restart: unless-stopped
  kibana:
    build:
      context: kibana/
      args:
        ELASTIC_VERSION: ${ELASTIC_VERSION}
    volumes:
      - ./kibana/config/kibana.yml:/usr/share/kibana/config/kibana.yml:ro,Z
    ports:
      - 5601:5601
    environment:
      KIBANA_SYSTEM_PASSWORD: ${KIBANA_SYSTEM_PASSWORD:-}
    networks:
      - elk
    depends_on:
      - elasticsearch
    restart: unless-stopped
networks:
  elk:
    driver: bridge
volumes:
  elasticsearch:

```


docker - compose 파일을 작성하는 방법은 따로 공부를 해야 하니 해당 코드에서, 몇가지 부분들만 체크하고 넘어가자 

```shell
    ports:
      - 9200:9200
      - 9300:9300
```

다음은 포트포워딩을 의미한다. 격리 컨테이너를 만든다는 의미는 격리컨테이너의 포트와 서버의 포트를 연결해야 한다는 의미이다, 다음의 그림과 같이 말이다. 

![[포트포워딩 1.png]]

컨테이너는 모두 개별포트를 가진다. guest가 접근 가능한 1차 포트는 host의 포트이기 때문에, 게스트가 호스트의 특정 포트로 접근할때 도커 컨테이너의 포트로 길을 안내해야한다. (포워딩) 이를 포트 포워딩이라 한다. 굳이 같은 포트 번호가 아니여도 된다. 예를들어 다음과 같이 20 : 30 으로 작성하면 host의 20번 포트로 들어온 요청은 내부적으로 도커컨테이너의 30번 포트로 들어간다. 

```
logstash:
    build:
      context: logstash/
      args:
        ELASTIC_VERSION: ${ELASTIC_VERSION}
    volumes:
      - ./logstash/config/logstash.yml:/usr/share/logstash/config/logstash.yml:ro,Z
      - ./logstash/pipeline:/usr/share/logstash/pipeline:ro,Z
    ports:
      - 5044:5044
      - 50000:50000/tcp
      - 50000:50000/udp
      - 9600:9600
    environment:
      LS_JAVA_OPTS: -Xms256m -Xmx256m
      LOGSTASH_INTERNAL_PASSWORD: ${LOGSTASH_INTERNAL_PASSWORD:-}
    networks:
      - elk
    depends_on:
      - elasticsearch
```

다음은 logstash의 컨테이너를 생성하는 부분이다 , 다양한 설정들을 컴포즈 파일에 미리 작성해두고, 컴포즈 파일을 docker-compose up 명령어만을 치면은 자동으로 설정해둔다. 이것이 도커컴포즈를 활요해서 환경을 구성하는 이유이다. 

## 해당 레포의 리드미를 따라서 설정을 마쳐보자 .

### 도커 돌리기

로컬에서 도커 실행시키기

1. 기존 도커 실행물들 모두 종료해주세요  
    1-1 도커 데스크톱 -> 컨테이너 -> 컨테이너 delete all
    
2. 다음으로 도커를 셋업하고 실행합니다.  
    docker-compose up setup -d  
    -> 도커 데스크톱에서 setup 도는지 확인해주세요  
    docker-compose up -d  
    -> 다음의 6가지 프로그램이 돌아야합니다.  
    모두다 돌았을때 다음의 상태가 됩니다.
    

[![](https://camo.githubusercontent.com/a19af56af4fdf8cb97208f21f0edc0d58ad04ae5fac9a79abe5f32ed84542584/68747470733a2f2f76656c6f672e76656c63646e2e636f6d2f696d616765732f6b6b6a353135382f706f73742f38366631633037362d313636632d343964662d386232642d6263366332393035643638342f696d6167652e504e47)](https://camo.githubusercontent.com/a19af56af4fdf8cb97208f21f0edc0d58ad04ae5fac9a79abe5f32ed84542584/68747470733a2f2f76656c6f672e76656c63646e2e636f6d2f696d616765732f6b6b6a353135382f706f73742f38366631633037362d313636632d343964662d386232642d6263366332393035643638342f696d6167652e504e47)

(셋업은 시간이 지나면 exited 상태가 됩니다. 이때까지 기다려주세요 )

#### 초기 설정
Kibana를 초기화하는 데 1분 정도 시간을 준 다음 웹 브라우저에서 [http://localhost:5601](http://localhost:5601/)를 열어 Kibana 웹 UI 에 액세스하고 다음(기본) 자격 증명을 사용하여 로그인합니다.

```
user: elastic
password: changeme
```
##### 사용자 인증 설정
터미널로 해당 디렉토리에서 다음 명령어 3가지로 비밀번호 재설정하고 이를 기록해주세요.

```
docker-compose exec elasticsearch bin/elasticsearch-reset-password --batch --user elastic
docker-compose exec elasticsearch bin/elasticsearch-reset-password --batch --user logstash_internal
docker-compose exec elasticsearch bin/elasticsearch-reset-password --batch --user kibana_system
```


env 파일 찾으셔서 열어줍니다. (이거 암호화 되어있는 경우가 있는데, 연결 프로그램을 메모장으로 변경하시면 암호화 풀립니다.)<br><br>[![](https://camo.githubusercontent.com/36efcf40cb59fed52b79076fe8564124d6b5b2a99d468c8d6c27fc6c8d326cca/68747470733a2f2f76656c6f672e76656c63646e2e636f6d2f696d616765732f6b6b6a353135382f706f73742f63313362653030302d383634622d346562372d613534662d6164613962623335303333662f696d6167652e504e47)](https://camo.githubusercontent.com/36efcf40cb59fed52b79076fe8564124d6b5b2a99d468c8d6c27fc6c8d326cca/68747470733a2f2f76656c6f672e76656c63646e2e636f6d2f696d616765732f6b6b6a353135382f706f73742f63313362653030302d383634622d346562372d613534662d6164613962623335303333662f696d6167652e504e47)<br><br>3가지 비밀번호 위에서 명령어로 비밀번호 변경된 부분(기록해두었던거) 로 바꿔줍니다.
```
docker-compose up -d logstash kibana 
```
해당 명령어로 elk 스택 재시작합니다.
```
user: elastic
password: <첫번째 명령어로 변경된 elastic 비밀번호>(메모장 첫번째)

```
웹 브라우저에서 [http://localhost:5601](http://localhost:5601/) 열어 Kibana 웹 UI를 실행 하고 다음 자격 증명을 사용하여 로그인합니다.

이러고 접속되면 elk 스택이 구성완료됩니다.<br><br>여기에서 유료정책만 basic 정책으로 변경해주세요.  <br>elasticsearch의 elasticsearch.yml 파일에서 해당 부분만 basic으로 변경해줍니다 . 
![[ELK설정.png]]