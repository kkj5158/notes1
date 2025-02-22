#ORM


# pre-compile 과정은 오류를 발생시킨다.

querydsl을 이용한 java project의 경우에는 gradle로는 과정이 조금 복잡해진다. 

다음의 오류가 계속 발생한다. 

Attempt to recreate a file for type

위 문제는 **query dsl에서 생성 해주는 Q Object(객체)** 관련된 문제입니다. 해당 에러가 발생하는 경우는 Q Object(객체)를 생성해야 하는데 이미 폴더나 객체가 생성되어 있어서 발생합니다. 새로운 파일을 생성하려고 하지만, 파일이 존재하여 파일을 덮어 쓸 수 없을 때 발생합니다.

<font color="#31859b">-> 즉, 덮어쓰기를 가능하게끔 만들어야 오류가 해결된다. </font>

# 빌드 과정에서 Clean 실행하기

해당 오류가 발생하면, 빌드과정에서 계속해서 이미 생성되어있는 QClass들을 Clean을 통해서 삭제한 후에 프로젝트를 실행시켜야 하는 치명적인 오류가 있다. 

