#Docker #DevOps 
# AWS EC2에 Docker 설치
[[AWS EC2 구축하기]]

- **명령어 사용 전 sudo를 쓰기 귀찮다면 아래 명령어 입력**

```shell
sudo su
```

![https://blog.kakaocdn.net/dn/cpduM3/btq8uavqvgJ/JTwk7lCPtHKnmU5nVNDfAK/img.png](https://blog.kakaocdn.net/dn/cpduM3/btq8uavqvgJ/JTwk7lCPtHKnmU5nVNDfAK/img.png)

**1) 필요한 Util 설치**

```shell
sudo apt update

sudo apt install apt-transport-https

sudo apt install ca-certificates

sudo apt install curl

sudo apt install software-properties-common
```

**2) curl을 통해 docker 설치 & apt 기능 추가**

```shell 
curl -fsSL <https://download.docker.com/linux/ubuntu/gpg> | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] <https://download.docker.com/linux/ubuntu> bionic stable"

sudo apt update
```

**3) Docker 설치**

```shell
apt-cache policy docker-ce
```

**4) Docker 다운로드 후 docker-ce 설치**

```shell
sudo apt install docker-ce
```

(참고 : 도커는 설치가 되면 자동으로 system service에 등록이 되기때문에 항상 실행 가능하다고 함)

# 도커 컴포즈 설치하기 

**도커 컴포즈 이용시에 업데이트된 버전을 깔아야 한다.**

apt install docker-compose 명령으로는 docker-compose의 최신 버전을 설치하지 못할 수 있습니다.

이 경우 최신 버전을 설치하는 방법입니다.

특정 버전을 사용하고 싶다면 VERSION 부분은 건너뛰고, sudo curl -L 이후의 ${VERSION} 부분을 원하는 버전으로 입력해주세요.

```bash
#버전확인
docker-compose -v
Docker Compose version [설치된 버전]

#기존 설치 삭제
sudo apt remove docker-compose -y

#jq library 설치
sudo apt install jq -y

#최신 버전 설치
VERSION=$(curl --silent <https://api.github.com/repos/docker/compose/releases/latest> | jq .name -r)
DESTINATION=/usr/bin/docker-compose
sudo curl -L <https://github.com/docker/compose/releases/download/${VERSION}/docker-compose-$>(uname -s)-$(uname -m) -o $DESTINATION
sudo chmod 755 $DESTINATION

#설치 버전 확인
docker-compose -v
Docker Compose version [최신버전]
```

실행 화면은 대충 아래와 같아요.(우분투 22.04 기준)

![https://blog.kakaocdn.net/dn/snOtY/btrN1f8V2ag/H3vJBjnYyYhbEsBpWmsFKk/img.png](https://blog.kakaocdn.net/dn/snOtY/btrN1f8V2ag/H3vJBjnYyYhbEsBpWmsFKk/img.png)

구축이 완료되었다면, 도커 compose yml 파일이 있는 곳에서 다음의 명령어로 docker compose 실행 .

```
docker-compose up -d
```
