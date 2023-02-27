---
marp: true
theme: uncover
class: invert
paginate: true
header: Marp tutorial
footer: 2023-02-14
---

# Unity 버전 설치


![h:400](./Unityimage/image.png) 

<!--h 높이조절 -->

Installs 누르기


---

![h:400](./Unityimage/ing.png) 
installs Editor 누르기

---

![h:400](./Unityimage/image2.png)
Archive를 눌러 Long-Term Support 눌러준다

 ---
 ![h:400](./Unityimage/image3.png)
 웹사이트에 들어갔으면 아래로 내려와 자신이 찾는 버전을 누른다

 
 ---
 ![h:400](./Unityimage/image4.png)
 Editor를 눌러준다 (참고로 맥북같은 경우 아래로 내리면 보인다)


 ---
![h:400](./Unityimage/image5.png)
다운로드 폴더에 들어가 실행시킨다.

 ---

![h:400](./Unityimage/image6.png)
설치중간에 자기 파일 위치는 어디있는지 알아야할 것

 ---
 
 ![h:400](./Unityimage/image7.png)
Locate를 눌러

 ---
 ![h:400](./Unityimage/image8.png)
 파일을 찾은 후 

 ---
  ![h:400](./Unityimage/image9.png)
  유니티를 눌러  select Editor 를 클릭

  ---
  ![h:400](./Unityimage/image10.png)
  그럼 설치가 완료 된 것을 확인할 수 있음

  ---

  # Dialogue
 ![h:400](./Unityimage/image11.png)
* window-asset store-Dialogue검색-Buynow 후 import


---
 ![h:400](./Unityimage/image12.png)
- imsport한 후 project창에 빈 곳을  오른쪽 마우스를 클릭 create 클릭 후 맨 위에 있는 pixelcrushers 클릭 후  Dialougue Syteam 클릭 후 Dialouge Database클릭

---

 ![h:400](./Unityimage/image13.png)
 - 만든 Dialouge Database를 더블클릭 후 Dialouge창을 game에 옮기고 Conversations 선택

---

  ![h:400](./Unityimage/image14.png)
  -  (+) 버튼을 눌러 New Conversation 1를 생성

---

 ![bg left height:4in](./Unityimage/image15.png)
![bg left height:4in](./Unityimage/image16.png)
 -  start 오른쪽 마우스 클릭 후 Create Child Node 클릭 node 생성

 ---
  ![h:400](./Unityimage/image17.png)
 -  Dialouge Text 입력 후 conditons에는 순서를 넣을 것 
 - conditons에서는  Variable["chapter"] == 0 and  기입
 - < start>를 시작 기점으로 변수 숫자는 0부터 시작해 0부터 넣을 것 
 


 ---
 ![h:400](./Unityimage/image18.png)
- node[END] 부분에서 다음 Node로 이동하기위해선
- script에서 Variable["chapter"] == 1  기입
- 플레이 버튼을 눌러 테스트 해볼 것 

---
![h:400](./Unityimage/image19.png)
* Conversations를 제작하다 복잡하게 배치할때

---

![h:400](./Unityimage/image20.png)
* < start>에오른쪽 마우스를 눌러 Arrange Nodes를 클릭

---
![h:400](./Unityimage/image21.png)
* Vertically(가운대 배치), Horizontally(좌쪽으로 배치)선택하여 클릭

----
![bg left height:4in](./Unityimage/image22.png)

![bg left height:4in](./Unityimage/image23.png)
이런식으로 배치가 가능

