
detached head
attached head 


checkout 자체가 head를 떼서 옮기는 개념 
branch는 꼬리표 개념 
commit id를 이름으로 저장해놓는 개념이 브랜치 

git reflog 

head가 이동한 history를 보여줌 '


**Fast-Forward 관계** 여부를 판단하는 것이 제일 중요하다. 

fast-forward merge -> 커밋을 꼬리표가 따라간다. 
- 앞선 커밋을 충돌없이 따라간다는 느낌 
- ff merge (기본)
- no ff merge 

- 두개를 명령어 입력해본적이 없는데? 

no ff 
- merge 커밋을 남겨야 반드시 병합이 가능한 관계 
- Fast-Forward와 반대로 충돌 없이 따라갈 수 없는 관계를 말한다.

즉 no ff는 3way merge 인가?? 

-

- **Fast-Forward 관계** 가 성립해야만 3way merge 는 no ff 머지 인가?? 
- 

3way merge가 기본 ?? -> 

-> 충돌이 발생하고, 이 충돌을 해결한 버전을 다시 만들어야 하므로 ff merge가 불가능하다. 
-> 



https://codingapple.com/unit/git-rebase-squash/