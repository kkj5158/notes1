#aws #DevOps 
## 💻 EC2 시작하기

### ✔️ 1. EC2 인스턴스 시작하기

- **EC2 인스턴스란 가상 컴퓨팅 환경**으로 가상 머신을 생성하고 실행하는데 사용된다.
    
- 웹 호스팅, 애플리케이션, 데이터베이스, 인증 서비스를 비롯해 **서버가 수행하는 모든 워크로드를 지원**한다.
    
> **![](https://velog.velcdn.com/images/kyj311/post/224621d5-bd81-483e-ac07-63993cfc7784/image.png)인스턴스 시작을 선택한다.**

### ✔️ 2. AMI (Amazon Machine Image) 선택하기

![](https://velog.velcdn.com/images/kyj311/post/62bdabc0-4a59-4476-94b0-7f5a20fab889/image.png)

출처-[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instances-and-amis.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instances-and-amis.html)

- **AMI란 인스턴스를 시작하는데 필요한 정보**를 제공하는 **이미지**로, 한 AMI로 여러 인스턴스를 생성할 수 있다.

- AWS에서 제공하는 **AMI를 선택하여 사용**할 수 있으며, **Linux/Windows**를 제공한다.
    
- **고유 이미지**를 생성할 수도 있고, **MarketPlace**에도 다양한 이미지가 존재하지만, 대부분 **유료**이기때문에 주의해야한다!
    

> **![](https://velog.velcdn.com/images/kyj311/post/e5407251-c69a-494c-a827-db386dccadf3/image.png)**
> 
> **AWS 프리 티어로 Amazon Linux 2 AMI(HVM)를 선택한다.**

### ✔️ 3. 인스턴스 유형 선택하기

- 각자 필요한 인스턴스의 성능과 크기에 따라 **적절한 유형을 선택**해야 한다!
    
- 인스턴스는 **5가지 유형**으로 나뉘며, 각 유형별로 **다양한 인스턴스 크기**를 제공한다.
    
    - 범용
    - 컴퓨팅 최적화
    - 메모리 최적화
    - 액셀러레이티드 컴퓨팅
    - 스토리지 최적화  
        [▶️ 인스턴스 패밀리 자세히 살펴보기](https://velog.io/@kyj311/AWS-%EC%BB%B4%ED%93%A8%ED%8C%85#%E3%85%87-ec2-%EC%9D%B8%EC%8A%A4%ED%84%B4%EC%8A%A4-%ED%8C%A8%EB%B0%80%EB%A6%AC)

> **![](https://velog.velcdn.com/images/kyj311/post/0b5c7e32-f8da-4bec-b3de-3adf87b9b231/image.PNG)AWS 프리 티어로 t2.micro 인스턴스를 선택한다.**

### ✔️ 4. 보안그룹 구성하기

- **보안그룹**은 EC2 인스턴스에 허용되는 인바운드, 아웃바운드 트래픽을 제어하는 **가상 방화벽**이다.
    
- 기본 보안 그룹은 모든 트래픽을 허용하며, **상태 기반 규칙**을 사용한다.
    

> **![](https://velog.velcdn.com/images/kyj311/post/9e890147-563d-409e-b71a-230839fe7c67/image.png)EC2 인스턴스는 터미널을 통해 접속해야 하기 때문에 SSH 22번 포트가 기본 값으로 설정되어있다.**

### ✔️ 5. 키페어 생성하기

> **![](https://velog.velcdn.com/images/kyj311/post/8eee7150-a830-4080-b5df-45fdb10505e2/image.png)이때 다운로드 되는 프라이빗 키 파일은 다시 받을 수 없기 때문에 꼭!! 안전하게 보안된 위치에 잘 저장해두어야 한다.**

### ✔️ 6. 인스턴스 시작하기

> **![](https://velog.velcdn.com/images/kyj311/post/f84ea237-83d7-4a8c-a7cf-343d78faf75f/image.png)다른 세부 설정들은 기본 값으로 두고 인스턴스 시작을 선택**

> **![](https://velog.velcdn.com/images/kyj311/post/bf19a84f-de4d-4877-95cd-e939a9a695eb/image.png)인스턴스가 성공적으로 생성된것을 확일할 수 있다!**

### ✔️ 7. 탄력적 IP 할당하기

- 인스턴스를 생성할 때는 항상 새 IP를 할당한다.
    
- 인스턴스를 중지하고 재시작하면 새로운 IP가 할당되기 때문에 고정적인 IP를 가질수 있고록 탄력적 IP 주소를 할당해 줄 것이다.
    
- 이때 탄력적 IP를 만들고 ec2에 연결해주지 않으면 과금이 되기때문에 주의해야한다!  
    **만들때는 과금이 안되지만 연결을 "안"하면 과금이 되니 주의**
    
    > ![](https://velog.velcdn.com/images/kyj311/post/902358ff-d8fe-45e9-bbf5-f547d72a74c6/image.png)![](https://velog.velcdn.com/images/kyj311/post/b631962b-4b7c-467a-af6a-3f91639358ac/image.png)![](https://velog.velcdn.com/images/kyj311/post/529c4497-ebda-468b-9ab5-ec9d0780fcfa/image.png)
    

### ✔️ 8. SSH 접속하기

> **![](https://velog.velcdn.com/images/kyj311/post/8670a762-c8e3-4495-8df7-ab7550163e03/image.png)**