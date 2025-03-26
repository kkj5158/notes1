#Spring 
### 참고자료
Spring Boot _ Quartz 배치 (scheduler) clustering
	https://kindloveit.tistory.com/95
# 문제사항 
Spring application을 구축하다 보면은 spring scheduler를 이용해서 cron job을 많이 사용하게 된다. 그러나 이중화나 쿠버네티스에서 여러 pod를 실행하게 되면 다수의 was에서 job이 중복해서 실행이 되게 된다. 이를 위해서 특정 Node의 was에서만 job을 실행되게 인자나 property를 뺄 수 있으나 배포시에 노드마다 설정을 지정해줘야 하는 번거로움이 생긴다. 

# 해결방법
Spring boot + Quartz 배치를 사용하고 Clustering 기능을 켜면 Cluster 기능으로 fail over를 방지할 수 도 있고 여러잡이 실행되는 것도 방지 할 수 있다. 

