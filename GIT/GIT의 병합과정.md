GIT에는 다양한 병합방법이 존재하고, 대표적으로 3가지로 나눌 수 있다. 
# 병합 방법

 1. Merge
	- ff merge
	- no ff merge 
2. Squash
3. Rebase  
## 1. Merge

## fast-foward관계란 ? 

### ff관계와 no-ff(3Way-Commit)관계
Git의 병합과정에 대해서 깊게 생각해본적이 없는데, 다양한 병합 과정이 존재한다는 것을 이번에 공부하다가 처음 알게되어서 정리해본다.가장 중요한 키워드는 ff 관계에 대한 이해이다. 

### ff(fast-foward)란?
말 그대로 커밋 기록을 따라잡는것을 의미한다. 

### ff 관계란? 
merge란 기본적으로 서로 다른 브랜치의 커밋내용을 비교하여서 커밋내용을 병합하는 과정이다. 이 과정에서 충돌이 발생하지 않는 관계. 즉 특정 브랜치가 베이스 브랜치에서 분기되어서 커밋을 쌓아나갈때. 아무런 충돌없이 따라잡기(fast-forward)가 가능한 관계를 의미한다. 

![[Pasted image 20250326120736.png]]

1. feature는 main으로부터 분기된 이후에 , A커밋과 B커밋을 쌓아나갔다. 
2. 자 여기서 main과의 병합을 생각해보자. 
3. main 과의 병합과정에서 충돌이 발생할 일이 없다. (main에서 따로 커밋을 만들지 않았다.)
4. 자 그러면 커밋을 main에 붙여서 fast-forward(따라잡기)만 하면된다. 
5. 이때 그러므로, commit-message를 굳이 남길 필요가 없다. (충돌 해결이  없으므로 ) 

다음의 경우에 main과 feature가 ff-관계에 있다고 말하며, ff 병합이 가능하게 되며, 일반적으로 ff 병합을 하게 된다. 

### no ff 관계란? 

ff 관계를 이해했다면 , 이제 no ff 관계는 더욱 쉽게 이해할 수 있다. 반대로 ff 관계가 성립되지 않는 경우. 즉 충돌이 발생하는 경우에 대해서 no ff 관계라고 정의내리는 것이다. 

다만 중요한점은  충돌이 굳이 발생하지 않는 경우에도 새로운 커밋 
즉 커밋을 따라잡기(ff)할 뿐만 아니라 병합커밋을 새로 만들고 싶은 경우에도 no ff 커밋을 임의적으로 사용할 수 있다는 것이다. 

![[Pasted image 20250326121156.png]]

### 결국 분류키워드는 병합시 브랜치사이의 충돌 여부와 새로운 병합 커밋메시지의 존재 유무이다. 
- 충돌 발생 -> 필수적으로 병합 커밋 새로 생성 : no-ff
- 충돌 발생x , 그럼에도 병합 커밋 새로 생성 : no-ff
- 충돌 발생x , 단순히 커밋을 따라잡기만 하고 싶음 , 병합 커밋메시지 생성없이 : ff 

## ff 병합과 no ff 병합
### 1-1. ff 병합 
![[Pasted image 20250326120736.png]]

위에서 설명한 그대로이다. ff관계가 성립할때. merge-commit을 남기지 않고. 커밋내역을 그대로 따라가면서 (fast-forward) 하는 병합과정이다. 보통 main과 main에서 분기한 feature 브랜치 사이에 충돌이 없을때 사용하는 병합 방법이다. 

### 1-2. no ff 병합 

![[Pasted image 20250326121156.png]]

역시 위에서의 no-ff 관계를 이해했다면 쉽게 이해할 수 있다. 
no-ff 관계가 성립할때 (병합 과정에서 충돌이 발생해서 새로운 커밋이 필수적일때) 혹은 임의적으로 병합과정을 하나의 커밋으로 남기고 싶을때 사용하는 병합방법이다. 단순히 커밋을 따라잡는것이 아니라 따라잡은 후에 새로운 병합 커밋이 발생한다. (여기서는 빨간색 커밋이 해당된다.)


### 1-3 추가적으로 no-ff 병합은 3Way-Merge이기도 하다. 

보통 no-ff 커밋은 다음의 그림과 같이 main(master) 브랜치로부터 새로운 브랜치가 분기되고 나서 (C2) master 브랜치 자체적으로 C4 커밋이 발생하고서 feature(iss53) 브랜치도 자체적으로 커밋을 쌓아나갈때 발생한다. 그러므로 더 이상 분기된 기점(C2)를 공통의 조상으로 가지지 않게 된다. 그러면 해당 병합에는 총 3개의 커밋이 관여하게된다. 공통분기점(C2) , master 자체의 커밋 (C4) , iss53의 커밋 (C5) 그러므로 3개의 커밋이 관여했으므로 3Way-Merge 으로 부르게 된다. 

![[Pasted image 20250326124413.png]]



### 추가 지식) ff, no-ff, 3way의 관계성 

ff와 no-ff 병합은 대비되는 관계이므로 교집합이 존재하지 않지만 3Way는 단순히 3개의 커밋이 병합되는 관계를 의미하므로 이 경우의 경우 관계성이 조금 복잡해진다. 

다음과 같이 이해해두자.

- 충돌의 여부와 병합 커밋메세지의 유무에 따라 ff , no-ff관계가 나뉜다. 
- 3way merge는 3개의 커밋이 관계되는 경우를 의미한다. 
- ff 병합과 3way 병합은 양립할 수 없는 병합이다. 
- no-ff병합은 보통 3way 병합이다. '
	- 하지만 반드시는 아니다. ff 병합이 가능함에도 임의적으로 커밋 메시지를 발생하는 경우는 2개의 커밋이 병합에 관여하지만 no-ff병합으로 보기 때문이다. 

##### 헷갈릴 수 있는 질문

Q1. 

내가 이해안가는건 개발자 A,B가 각각 main 브랜치에서 f1, f2로 분기해서 A가 먼저 f1을 병합시키고, 그다음에 B가 f2를 병합해도 충돌이 없다면 merge commit 없이 병합이 가능한데 이럴경우에도 ff merge라고 볼 수 있는거 아냐? (즉 3way merge이면서 ff merge일 수 있는거 아냐? 3way merge와 ff merge는 양립이 안된다면서?)

A1. 

부분적으로 보시면 해당 merge는 3way-merge가 아닙니다. main , f1, f2를 기준으로 보시면 3way라고 느껴질수 있지만 3way의 기준은 병합시점 관여 커밋의 갯수입니다. 첫번째. A 개발자가 main 브랜치에 병합할때 main브랜치에 새로운 커밋이 존재하지 않으므로 분기점 커밋 , f1 브랜치의 최신 커밋까지의 내역으로 2개의 커밋이 관여하게 됩니다. 이때 main브랜치에서 새로운 커밋이 발생하지 않았으므로 ff 병합이 한번 발생합니다. 그리고 나서 B개발자가 main에 병합을 시도하면 (main 병합지점을 pull 로 흡수했을때를 기점으로) main에 새로운 커밋이 있더라도(f1의 커밋 흡수) 이미 병합이 완료되어 있기 때문에 하나의 커밋으로 여겨지고 다시 f2하고의 2개의 커밋을 기준으로 ff 병합을 하게 되는 것입니다. 

A2. 추가 질문: **3-way 병합이 발생하는 경우는?**

만약 B가 `f2` 브랜치에서 `f1`의 변경 사항을 포함하지 않고 작업을 계속했다면, `f2`를 `main`에 병합할 때 **3-way 병합이 발생**할 수 있습니다.

- 이 경우, Git은 `main`과 `f2`의 공통 조상(common ancestor)을 찾아 변경 사항을 비교하고,
    
- 새로운 병합 커밋(merge commit)을 생성하는 **3-way 병합**을 수행해야 합니다.
    

즉,

- **FF 병합이 가능하면 merge commit 없이 진행됨.**
    
- **FF 병합이 불가능하면 3-way 병합이 수행되면서 merge commit이 생성됨.**
    

✔ 현재 질문에서는 **FF 병합이 가능했기 때문에, 3-way 병합 없이 두 번의 FF 병합이 일어난 것!** 🎯 그러므로, ff 커밋과 3-way커밋은 양립할 수 없는 커밋 형태입니다!. 


## 2. Squash 병합 

![[Pasted image 20250326121641.png]]

Squah Mereg는 feautre의 모든 커밋을 하나의 커밋으로 만들어서 main에 머지하는 방법이다. 단순히 fast-forward(따라 잡기) 커밋이 아니므로 no-ff 머지인 동시에 feature에서의 모든 커밋이 하나의 커밋으로 합쳐진 새 병합 커밋이 만들어지게된다. 이점이 기본 no-ff merge와의 차이점이다. 

**보통 실무에서는 feature 브랜치에서 리뷰 반영, 버그 수정등으로 쓸데없는 커밋이 많아진 경우 이를 다 기록하지 않고 하나의 새로운 커밋으로 통합해서 남길때 사용하게 된다.** 

Squah merge는 반드시 새로운 통합 커밋메세지가 발생하므로 no-ff 머지이다. 

## 3. Rebase 

**이름을 봤을때 병합(merge)이 아니라 생각하는 사람이 맞지만 rebase도 엄연히 두개의 브랜치를 병합하는 하나의 명령어임을 명심하자** 

![[Pasted image 20250326121911.png]]


```git
$ git switch main 
$ git rebase feature
```

해당 경우는 main에 아무런 추가 커밋이 없다면 ff와 동일하게 HEAD만 이동하게 된다. 이는 rebase의 뜻을 생각해보면 쉽게 이해할 수 있다. 분기 기점(base)를 다시(re) 배치한다는 뜻으로. 분기 기점으로부터 분기된 브랜치의 커밋내역을 분기기점과 새로운 커밋을 기준으로 사이에 흡수해버리고 브랜치의 분기기점을 다시 배치시켜버리는 것이다. 

별도의 Merge Commit이 남지 않는다는 점은 ff 관계에 성립하지만 Rebase는 각 브랜치에 다른 커밋이 있어도 하나의 줄기로 합쳐줄 수 있다는 장점이 있다. 

### Rebase를 사용하는 이유 

앞에서 말했듯이 3way-merge가 발생하는 경우 

![[Pasted image 20250326132110.png]]

위의 그림과 같이 공통의 조상 분기점을 가지지 않고 master가 독자적으로 커밋을 쌓은경우에 3way-merge를 하게 된다. 

이 3way-merge의 단점은 Merge Commit을 반드시 생성해야하고 그리므로 merge 이력이 쌓이고 쌓여서 아래처럼 커밋 트리가 복잡해진다는 것이다. 

![[Pasted image 20250326132252.png]]

이러면 이전 커밋에서 문제가 생겼을 경우 추적하는 것도 힘들고 단순히 "A와 B가 머지되었다"를 상지앟는 머지 커밋을 쌓아두는 것도 너무 쓸데없이 많아진다는 점이 문제로 발생한다.

이럴때 필요한게 Rebase Merge이다.

![[Pasted image 20250326132407.png]]
![[Pasted image 20250326132411.png]]

Rebase는 다음과 같이 기존의 조상 분기점(C2)를 master의 C3분기점으로 재배치시키고 거기에 C4의 커밋을 더해서 적용시킨다. 그러므로 조상(베이스)가 달라지는 것이다. 

그럼 리베이스를 하는 순간 experiment(C4)와 master(C3)의 조상은 같아지고

거기서 머지를 하면 experiment(C4)가 Fast-forward 가 된다.

이러면 머지 커밋도 생성되지 않고
커밋 트리가 선형으로 매우 깔끔해진다.

### 헷갈릴 수 있는 질문 

#### rebase시에 커밋 순서 ? 


![[Pasted image 20250326121911.png]]


![[Pasted image 20250326132411.png]]

rebase시에는 main브랜치에 feature브랜치가 흡수될때 커밋순서는 커밋시간을 기준으로 이루어집니다. 그러므로 다음의 두 그림 모두 맞는 그림입니다. rebase핵심은 main브랜치에서 새로 발생된 커밋을 새로운 베이스 지점으로 삼는 커밋이라는 점입니다.  그러므로 무조건 새로운 베이스와 기존의 feature 브랜치의 커밋 2가지만을 비교하므로 3way-merge가 아닙니다. 

#### 🔍 **왜 Rebase는 3-way Merge가 아닐까?**

##### ✅ 3-way 병합의 핵심

3-way 병합은 **공통 조상(common ancestor)**을 기준으로 **현재 브랜치(A)와 병합할 브랜치(B)의 변경 사항을 비교**하여 **새로운 병합 커밋을 생성하는 과정**입니다.  
즉, **A, B, 공통 조상(총 3개의 commit 정보)을 사용하여 새로운 commit을 만든다**는 점에서 "3-way merge"라고 합니다.

##### ❌ 하지만 Rebase는?

- Rebase는 **기존의 커밋을 유지하지 않고 새로운 커밋으로 재작성**합니다.
    
- **병합 커밋을 생성하지 않고, 개별 커밋을 새로 적용하는 방식**입니다.
    
- 따라서 **공통 조상을 기준으로 한 3-way 병합이 발생하지 않습니다.**
    
- 대신, **각각의 커밋을 순차적으로 적용(replay)하는 과정**에서 충돌이 발생할 수 있습니다.
    
- 만약 충돌이 발생하면, 사용자는 **각 커밋마다 충돌을 해결해야 함** (하지만 이것도 3-way 병합과는 다름).
    

---

##### 🔥 **결론**

> **"Rebase는 3-way merge가 아니겠네?"**  
> ✅ **그렇다!**  
> ✔ Rebase는 **기존 커밋을 재배치하는 방식이므로 3-way 병합을 수행하지 않음.**  
> ✔ **병합 커밋(merge commit)이 생성되지 않으며, 히스토리가 깔끔하게 유지됨.**  
> ✔ 하지만 충돌이 발생하면 사용자가 **각 커밋별로 해결해야 함.** 🚀
