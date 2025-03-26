#DB 

dbeaver에서 postgres나 mysql db를 빠르게 백업하고 복구하는 방법을 알아봅시다. **중요한 것은 db 서버 버전하고 dbeaver쪽이 인식하는 client 버전하고 맞춰줘야 한다는 점이 있음,**

![https://blog.kakaocdn.net/dn/boDb8u/btrKwG90NX2/G7BhTBMq2xLMYOX4Bk1Qs1/img.png](https://blog.kakaocdn.net/dn/boDb8u/btrKwG90NX2/G7BhTBMq2xLMYOX4Bk1Qs1/img.png)

먼저 db를 우클릭 한 다음에 도구 - 백업을 선택합니다.

![https://blog.kakaocdn.net/dn/cSunje/btrKvPfdZB8/jVPRr5gxO0EmlLVdSKJHhk/img.png](https://blog.kakaocdn.net/dn/cSunje/btrKvPfdZB8/jVPRr5gxO0EmlLVdSKJHhk/img.png)

그러면 export를 할 오브젝트를 선택하라고 나옵니다. public 데이터베이스를 선택했습니다. 그랬더니, auth_group, auth_user 등 테이블들이 있는데요. 이들을 선택하면 테이블에 있는 데이터들을 쉽고 빠르게 백업할 수 있게 됩니다.

![https://blog.kakaocdn.net/dn/U4ITI/btrKwGa6Ryi/XOVy03wyfl1Ub3kK8Ojle1/img.png](https://blog.kakaocdn.net/dn/U4ITI/btrKwGa6Ryi/XOVy03wyfl1Ub3kK8Ojle1/img.png)

다음을 누르면, Format을 설정하고, 옵션들을 선택하는 것이 나옵니다. 옵션 선택지는 디폴트로 설정하였습니다. 그리고 Format은 Custom으로 설정하였습니다. Custom으로 설정이 된 경우, 아마 바이너리를 떨어트리는 듯 합니다. 권한이라던지, 테이블 owner 등을 백업하지 말 것인지 등을 선택할 수 있습니다. output folder를 설정하고 Start를 누릅니다.

![https://blog.kakaocdn.net/dn/2klsR/btrKuKThIVl/P4bEq1oxmGjWj00YXKb4Q1/img.png](https://blog.kakaocdn.net/dn/2klsR/btrKuKThIVl/P4bEq1oxmGjWj00YXKb4Q1/img.png)

다 되었다면, 설정한 경로에 dump가 생성되었음을 볼 수 있습니다.

---

이제 post에 있는 내용들을 모두 삭제해 보겠습니다.

![https://blog.kakaocdn.net/dn/vFVIO/btrKwbvEKx5/5c246Kye1fM89wFNtRdSIk/img.png](https://blog.kakaocdn.net/dn/vFVIO/btrKwbvEKx5/5c246Kye1fM89wFNtRdSIk/img.png)

포스트 테이블에는 이런 데이터들이 있는데요. 데이터베이스에 있는 데이터를 모두 날려보겠습니다.

![https://blog.kakaocdn.net/dn/bIAK2I/btrKuwgHFap/kYVMyd7PHK9mzOfRDvKYh0/img.png](https://blog.kakaocdn.net/dn/bIAK2I/btrKuwgHFap/kYVMyd7PHK9mzOfRDvKYh0/img.png)

아앗.. 데이터베이스가 날라갔으니 망한 걸까요? 아닙니다. 복원을 하면 됩니다. 다시 데이터베이스 우클릭 하고, 도구 - 복원을 눌러보겠습니다. 영어라면 tools - restore database입니다.

![https://blog.kakaocdn.net/dn/d4ulIC/btrKsPt2AHE/M9mKQxbkvNTzft1UatvmO0/img.png](https://blog.kakaocdn.net/dn/d4ulIC/btrKsPt2AHE/M9mKQxbkvNTzft1UatvmO0/img.png)

복원을 클릭합니다.

![https://blog.kakaocdn.net/dn/bqDUwH/btrKwh3DUeg/dEGKBrcDRvbtCpJB4rJFZ1/img.png](https://blog.kakaocdn.net/dn/bqDUwH/btrKwh3DUeg/dEGKBrcDRvbtCpJB4rJFZ1/img.png)

백업 파일을 선택합니다. 덤프 파일이 dump-test-202208240006이였으므로, 이것을 선택한 후에, Start를 누릅니다.

![https://blog.kakaocdn.net/dn/BoI1D/btrKuKsdm8t/SraWzcGpLSumYKR1ANXWw1/img.png](https://blog.kakaocdn.net/dn/BoI1D/btrKuKsdm8t/SraWzcGpLSumYKR1ANXWw1/img.png)

다시 저장되어 있는 포스트를 확인해 보면, restore가 되었음을 알 수 있습니다.

---

mysql도 비슷한 방식으로 하면 되니 별 문제는 없습니다. LocalClient 버전과 서버 버전이 달라서 에러가 발생하는 경우가 종종 있는데요. 비슷한 문제 상황을 mysql 데이터를 export 하면서 재현시켜 보겠습니다.

![https://blog.kakaocdn.net/dn/dcywYq/btrKwjf5tl8/j709UnvO2KmECAxM9nGuY1/img.png](https://blog.kakaocdn.net/dn/dcywYq/btrKwjf5tl8/j709UnvO2KmECAxM9nGuY1/img.png)

mysql 디비에 접근해서 export를 하려고 합니다. 평소와 같이 디폴트 값으로 설정해 두고, Start를 눌러 보겠습니다.

![https://blog.kakaocdn.net/dn/bjJSsd/btrKvcBT9RF/x3M5tq5CnjiluDeWKIwN71/img.png](https://blog.kakaocdn.net/dn/bjJSsd/btrKvcBT9RF/x3M5tq5CnjiluDeWKIwN71/img.png)

어? Export를 하는데 이상한 에러가 떴습니다. 사실 저는 mysql server 8.0.30 버전이 설치된 db 서버에 있는 데이터를 export 하려고 했는데요. caching_sha2 관련 에러가 뜬 걸로 보아서는 dbeaver가 인식하는 드라이버 버전과 맞지 않아서 발생한 듯 해 보입니다. 제 경우에는 그랬습니다. 실제로 버전 체크를 해 본 결과 5.5대였습니다.

![https://blog.kakaocdn.net/dn/tQnTR/btrKuUnQwH5/NkplnHwYKFSHWyuWfkkJX1/img.png](https://blog.kakaocdn.net/dn/tQnTR/btrKuUnQwH5/NkplnHwYKFSHWyuWfkkJX1/img.png)

그러면 어떻게 해야 할까요. 버전이 동일한 mysql을 설치한 후에, client home 경로를 추가해 주겠습니다.

![https://blog.kakaocdn.net/dn/u9rzn/btrKuSDETtH/tkfzzTCtwHHVsGXVwMrrS1/img.png](https://blog.kakaocdn.net/dn/u9rzn/btrKuSDETtH/tkfzzTCtwHHVsGXVwMrrS1/img.png)

Local Client 클릭 후, 열기 ... 를 선택하시면 아래와 같은 창이 등장합니다.

![https://blog.kakaocdn.net/dn/bmHKoP/btrKwbCtlTW/9PP4lmXVNRgCOsa0ymQoIk/img.png](https://blog.kakaocdn.net/dn/bmHKoP/btrKwbCtlTW/9PP4lmXVNRgCOsa0ymQoIk/img.png)

여기서 홈 추가 누르시고, mysql의 bin 경로를 넣어주시면 됩니다.

![https://blog.kakaocdn.net/dn/bUXUPz/btrKwiVNkPD/iA5QGTOAhuPtbr5vyODZX0/img.png](https://blog.kakaocdn.net/dn/bUXUPz/btrKwiVNkPD/iA5QGTOAhuPtbr5vyODZX0/img.png)

그리고 나서, Start를 누르시면 export가 됨을 알 수 있어요.