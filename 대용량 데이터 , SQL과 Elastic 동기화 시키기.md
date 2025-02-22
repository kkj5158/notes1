#DB 

1000만건이 넘는 도서데이터를 SQL데이터베이스에서 , Elastic Search로 옮기려고 한다. 이때 Logstash를 통해서 데이터를 동기화해보는 과정에 도전해보자 . 

참고자료
	https://www.elastic.co/kr/blog/how-to-keep-elasticsearch-synchronized-with-a-relational-database-using-logstash


Elastcis Search가 제공하는 강력한 검색기능을 활용하기 위해서 , 수많은 기업들이 기존의 관계형 데이터베이스와 동시에 ElasticSearch를 사용한다. 이때 두 데이터베이스의 상태를 유지해야할 필요성이 있다.
[[SQL과 ES 병행사용에 대한 고찰 1]]

