---
marp: true
theme: cover
class: invert
paginate: true
header: Marp tutorial
footer: 2023-02-13
backgroundColor: 
---
<!--_color: pink-->
# Unity VR Programming

---

# 목차
* 오큘러스 간단한 용어 설명

*  캐릭터 모델링 Unity로 import

*  트리거 기능(가방안에 물건 고정하기)
* 오큘러스 퀘스트2 세팅 + 핸드 트래킹 절차 안내
* Oculus Quest2 사이드퀘스트 설치 및 활성화
* Unity VR 다양한 씬 체험설명
* HandTrackingEvent
* Scene 이동
* 오류 및 해결내용

---

# 오큘러스 간단한 설명

*  VR(가상현실): 현실과는 다른 가상세계에서 실제같은 경험을 느낄 수 있는 기술
* Oculus link: 케이블을 통해 PC와 연결할 수 있는 기능(PC VR모드로 전환)
*  PassThrough: 고글에 탑재된 카메라를 통하여 주변환경을 흑백으로 송출해주는 기능
*  Chrome Cast: 폰, 탭, 노트북, VR 등 다양한 디스플레이 기기들을 TV로 송출 수있도록 도와주는 하드웨어 기기
*  Oculus Developer Hub: 오큘러스 퀘스트에서 앱을 개발하거나 라이브 스트리밍을 더 편리하게 사용할 수 있는 PC어플 
* 룸 스케일 경계 / 고정 경계: 오큘러스같은 VR을 사용하기 위해선 임시 공간

---

* Hand Tracking
핸드 트래킹은 오큘러스 고글에 탑재된 있는 4개의 카메라와 센서를 통하여 손을 감지기능
[핸드 트리킹 관련영상1](https://youtu.be/hX7GJfYmj7M?t=662)
[핸드 트리킹 관련영상2](https://www.youtube.com/watch?v=WELSs-lPJYA)
---

# TouchGrab(자유자재로 잡기 기능)

* game object(1)를 만들고 물건의 이름으로 변경.
* Touch hand Grab Interactable, Rigidbody, Grabbable, Physics Grabbable, Respawn On Drop을 추가.
* 그 안에 모델링 된 물건을 넣는다.
* 그리고 그 안에 game object(2)를 하나 더 만들어서 물건이름_collider 으로 변경.
---

![h:400](./project1/image.png)
game object(2)에
mesh filter을 추가하여 mesh에 cube를 넣고(mesh filter가 이미 있다면 넣지말것),
box collider을 추가하여 edit collider를 누르고(또는mesh collider 추가)

---
![h:400](./project1/image2.png)
물건에 최대한 맞게 박스를 조정.

---
![h:400](./project1/image3.png)
다시 game object(1)로 가서 
위 사진과 동일하게 설정한다. 
Touch Hand Grab Interactable - Pointable Element에 game object(1)을 드래그드롭

---
bounds collider에 game object(2)를 드래그드롭 
Grabbable - Transfer On Second Selection 체크
Physics Grabbable - Grabbable과 Rigidbody에 game object(1)드래그드롭
Respawn On Drop - 0.1로 설정
(만약 Rigidbody에 Use Gravity가 꺼져있다면 꼭 체크하기)

---
### Colliders 만들기 (HullPart)
![bg left height:4in](./project1/image4.png)
 1. game object(2)는 잡을 수 있는 범위였다면 이번에 제작하는 것은 잡을 수        있는부위이다.
물건에 Mesh Collider을 추가.




2. Mesh Collider - Convex 체크
   물건에 부착되어 있는 부분(단추, 끈 등)도 잡는기능을 추가하고 싶다면 위 방법을 반복.

---
# 예시)
![h:400](./project1/image5.png)

---
![bg left height:4in](./project1/image6.png)
다시 game object(1)으로 돌아가서 
Touch Hand Grab Intereactable - Colliders 에서 
1. 물건 포함 파츠들의 총 수
2. Hierachy에서 HullPart들을 하나씩 드래그드롭
(만약 잡는 부분이 서로 다른위치에 있다면 touch hand grab interactable 
스크립트를 하나 더 추가하여 기능을 넣는다)

---
## 오류보완>collider가 충족되지 않을 경우
![h:400](./project1/image7.png)

이 경우, Bounds Collider가 none 또는 Colliders가 none 이였기에 발생하는 
오류로, 게임이 전혀 작동되지 않는다.

---
## OVR Build - 빌드에서 핸드트래킹 기능이 작동되지 않는다면?

![h:400](./project1/image8.png)
Hierachy - Headset(VR카메라) - OVR Camera Rig - Inspector - 내려가면 Quest Features - Hand Tracking Support - Controllers and Hands로 바꾸기

---
## Convex 오류
![h:400](./project1/image9.png)
touch hand grab interactable을 추가하여  bounds collider와 colliders - element0 에 가방hierachy를 모두 넣는다.

---
## 담기는 기능을 넣는 방법
![h:400](./project1/image10.png)

필요한 것: 오브젝트의 mesh와 모델링 파츠들

---

## 오브젝트가 잘 안잡히는 이유

* 사이즈가 너무 커서 잡는 범위 또한 커져서 어렵기 때문
* 범위를 작게 잡았기 때문에
* 등록한 '잡을  수 있는 부위'가 너무 작게 지정되었거나 부위의 콜라이더를 잘못 
설정했기 때문


---

## 잡기 기능 늘리기-ex))마스크
![h:400](./project1/image11.png)

---
1. mask_collider 에 가장 위에 있는 콜라이더를 없앤다
2. mask - inspector - touch hand grab interactable - colliders - element +버튼누르고 추가 - mask_collider을 element3에 끌어넣는다

3. mask_collider (2)에서 is trigger 체크한다 - istrigger로 지정해 두면 모델링 부위까지 손이 닿고 잡아야 잡히는 자연스러운 기능을 넣을 수 있다.(안할 시 콜라이더 부분이 먼저 인식되어 손에 쉽게 밀려나가고 부자연스럽다)



---

# 트리거 기능(가방안에 물건 고정하기)

---

![bg left height:4in](./project1/image12.png)
1. 가방오브젝트에 gameobject(이름:collider) 
2. rigidbody추가에 IsKinematic체크하고, box_collider을 가방내부에 맞춰 생성하고 IsTrigger 체크를 한다.(가방의 모델링이 박스가 아닌 다른 유형을 갖고 있다면 가방 내부 모델링을 받아 콜라이더로 지정하거나 전반적인 사이즈로 지정하나 들어간 사물들이 가방을 뚫고 있을 수 있다)

---
3. 스크립트 BagInScript를 생성한다.(Teams 파일에 업로드됨)
Card_collider에는 들어갈 사물의 collider, Card_g에는 사물(gameobject), In_target에는 가방, Out_target에는 사물의 부모를 지정한다.
4. 물건이 plane 부분에 가까우면 리스폰되기 때문에 plane을 낮추거나 수치를 조정해야한다
* 가방안에 물건이 들어갈 시 parent가 정상적으로 작동되지만 들어가있는 물건은 잡기기능이 비활성화되어있다. 
5. 콜라이더 작용으로 인해 손으로 물건을 들어올릴 시 'card out bag!' 로그가 뜨며 잡기기능이 정상작동 된다.
(OnTriggerExit:b_l_() - 손으로 가방에 상호작용을 할 때 마다 로그가 뜨는 현상이 있다.)


---

# 오큘러스 퀘스트2 세팅 + 핸드 트래킹 절차 안내

---

## [유니티 허브 다운로드(Download)](https://unity3d.com/kr/get-unity/download)
* Unity Hub 다운로드 클릭 → UnitySetup 설치

---

# 유니티 버전 설치
![h:400](./project1/image13.png)



---

![h:400](./project1/image14.png)


---
![bg left height:4in](./project1/image15.png)(예시사진)

1. 플랫폼(PLATFORMS)에서
 Android Build Support, Android SDK & NDK Tools, OpenJDK 선택하기 
 2.  계속(Continue)

3. 약관 동의 → 설치

---
# ※ 해당 버전이 없을 경우
<div>
<a target="_blank" href="https: //github.com/whj11201/whj11201.github.io/blob/main/Unityinstalls.md">해당 폼랫폼이 없을시 방법</a> 
</div>

---

# VR 프로젝트 생성

![bg left height:4in](./project1/image16.png)
1. 유니티 허브(Unity Hub) 메인 창
2. 좌측 메뉴바의 프로젝트 클릭
3. 새 프로젝트(New project)
4. VR (템플릿 없을 경우 템플릿 다운로드 클릭)
5. 프로젝트 이름(Project Name)
6. Basic VR  →위치(Location) 
7. 파일 위치는 원하는 곳에 지정
8. 프로젝트 생성(Create Project) 

 ---
 
# 프로젝트 생성 후
![bg left height:4in](./project1/image17.png)

1. Project > Assets > Scene 으로 이동 → 우클릭 → Create → Scene 생성(이름은 VR Basic)

2. 더블클릭하여 씬(Scene) 들어가기

---
![bg left height:4in](./project1/image18.png)
3. VR Basic 씬(Scene) 
4. 3D Object 
5. Plane 생성하기

---
![bg left height:4in](./project1/image19.png)
 6. Hierarchy창에 Main camera 삭제(Delete)
7. Project창에 grid 검색 후 창에 보이도록 세팅 

---
## Oculus Integrations 설치


![h:400](./project1/image21.png)

1. Window에서 Asset Storer

---
![h:400](./project1/image20.png)
2. [Oculus integration 검색](https://assetstore.unity.com/?q=Oculus%20Integration&orderBy=1)

---
![bg left height:4in](./project1/image22.1.png)
3. Oculus integration 클릭 
4. 에셋 다운로드(Asset download) 
5. Unity에서 열기(Open Unity)
6. 유니티 에디터 열기(유니티에서 Package Manager 실행)
(Sign in을 해야 다운로드 가능)

---
![h:400](./project1/image22.png)
Oculus integration 클릭 → Download → Import

---

![bg  w:300](./project1/image23.png)
![bg  w:300](./project1/image24.png)
![bg  w:300](./project1/image25.png)
![bg  w:300](./project1/image26.png)

---

#### 알림창 - Yes > Cancel > Ok > Restart > Upgrade → 유니티 재시작 후 Import 완료

 ---
## 만약 알림창이 Upgrade가 아닌 경우
![h:400](./project1/image27.png)
* Show Assets (Recommended)  > Delete Assets (Recommended) - Upgrade로 변경 완료 
 
 ---
 # VR 카메라 추가
 ![bg left height:4in](./project1/image28.png)
 1. Project Scenes(꼭 VR Basic씬 안에서 검색해야 함) 
 2. OVRCameraRig 검색 → Hierarchy창에 드래그 
3. Headset으로 이름 변경

---
 ![bg left height:4in](./project1/image29.png)
4. HeadSet 클릭 → OVR Manager (Script) → 
5. Tracking Origin Type - Floor Level 설정 →
6. Hand Tracking Support - Hands Only, Hand Tracking Frequency - MAX 로 설정

---
 
 # VR 핸드 추가
![h:400](./project1/image30.png)
1. Project -Scenes - OVRHandPrefab 검색 

2. LeftHandAnchor, RightHandAnchor에 각각 OVRHandPrefab을 드래그하여 추가

---
![bg left height:4in](./project1/image31.png)
  3. OVRHandPrefab 를 각각 LeftHand, RightHand로 이름 변경

  
  ---

![bg left height:4in](./project1/image32.png)
4. LeftHand 클릭 → OVR Skeleton 스크립트  > Update Root Scale 체크
5.  Enable Physics Capsules 체크 
6. OVR Mesh 스크립트 > Mesh Type - Hand Left 설정

---

![bg left height:4in](./project1/image33.png)
7. RightHand 클릭 → OVR Skeleton 스크립트  > Update Root Scale 체크, Hand Right 설정
8. Enable Physics Capsules 체크 
9. OVR Mesh 스크립트 > Mesh Type - Hand Right 설정

---

# Oculus Quest2 사이드퀘스트 설치 및 활성화

### 1. [오큘러스 개발자 계정 등록하기](https://developer.oculus.com/manage/organizations/create/)

---

![bg  w:500](./project1/image34.png)
![bg  w:500](./project1/image35.png)
![bg  w:400](./project1/image36.png)

---
* 단체 만들기 → 단체 이름 설정 →  I understand 체크하기 → 제출 클릭 → 동의함(개발자 비밀 유지 동의서) 클릭 → 제출
 
* 페이스북 로그인 아이디가 번호(본인 휴대폰)계정이 아닐 때, Oculus페이지 내에 번호 추가하기

---

# 오큘러스 퀘스트2(Android) 개발자 모드 활성화

![h:400](./project1/image37.png)
Oculus 앱 → 메뉴 → 기기 → 개발자 모드 → 개발자 모드 ON

---
# 사이드퀘스트 설치
![bg left height:4in](./project1/image38.png)
[링크](https://sidequestvr.com/download)
Advanced Installer ( LTS ) 버전으로 설치
(Easy Installer(Beta)는 테스트용이기 때문에 쓰지 말 것)
DOWNLOAD FOR WINDOWS 설치

---
# 오큘러스 퀘스트2 USB 디버깅 활성화
![h:400](./project1/image39.png)
 
* 퀘스트2 옆면에 있는 USB단자에 USB-C 케이블을 꽂아 PC와 연결 → VR에서 USB 디버깅 활성화 문구 동의(문구가 뜨지 않을 경우 재부팅)

---

![bg  w:500](./project1/image41.png)
![bg  w:400](./project1/image42.png)

---

디버깅 활성화 시 사이드 퀘스트 상단 아이콘이 주황불에서 초록불로 변경 후 

![h:400](./project1/image40.png)
VR 내에서 해당 문구가 뜹니다. 
 
USB 디버깅을 허용하시겠어요? (허용 클릭) / 데이터 액세스 허용합니다. 허용

---

![bg left height:4in](./project1/image43.png)
![bg left height:4in](./project1/image44.png)

1. 사이드 퀘스트에서 상단 메뉴 TV 모양 아이콘 클릭 
2. 해당 창이 뜸 
3. QUEST 2 CROP 클릭 
4. START STREAM 클릭

---
# Unity VR 다양한 씬 체험설명

Assets > Oculus > Interaction > Sameples > Scenes > Examples 로 들어가기


---

### 1) DistanceGrabExamples

![bg left height:4in](./project1/image45.png)


* 멀리 있는 물체를 집을 수 있고, 표시되는 UI가 사물마다 다름.

---
### 2) GestureExamples
![bg left height:4in](./project1/image46.png)

* 오브젝트와 핸드트래커에 강한 충격을 주면 색이 변함

---

### 3) HandGrabExamples

![bg left height:4in](./project1/image47.png)
* 오브젝트를 잡을 때 빛이 밝아짐 
* 횃불의 불이 따라오는 효과
* 손의 각도에 따라 컵을 다르게 집음

---
### 4) PokeExamples

![bg left height:4in](./project1/image47.png)
* 빨간 버튼을 누를 수 있는 기능(UX.UI 참고)
* 버튼 오버 기능(오버했을 때 색이 밝게 변화)
* 스크롤 기능
* 다양한 위치의 버튼 UI

---

### 5) PoseExamples

![bg left height:4in](./project1/image48.png)

* 손 제스처에 따른 다양한 이펙트 효과

---



### 6)  RayExamples
![bg left height:4in](./project1/image49.png)
![bg left height:4in](./project1/image50.png)

* 인터페이스 불투명 정도

---
### 7) TouchGrabExamples


* 중력 적용 오브젝트, 미적용 오브젝트
![bg left height:4in](./project1/image52.png)
![bg left height:4in](./project1/image51.png)

---

### 8) TransformExamples

![bg left height:4in](./project1/image53.png)

---
![bg left height:4in](./project1/image54.png)
* 문 열기 기능

---

![bg left height:4in](./project1/image55.png)

* 오브젝트를 다른 오브젝트 안에 넣기

---
![bg left height:4in](./project1/image56.png)
![bg left height:4in](./project1/image57.png)

* 이미지 갤러리를 볼 수 있는 인터렉션 기능

---

### 1).Unity Universal RP 설치 및 Import

1. Package Manager에서 Import하기
![h:400](./project1/image58.png)
window - Package Manager - Universal RP - Install - Import
※ 좌측상단에 Packages에서 Unity Registry 로 설정하기

---

### 2). Assets창에서 Rendering 설정

 ![h:400](./project1/image59.png)


 ---
![h:400](./project1/image60.png)
Asset창에서 우클릭 후 - Create - Rendering - universal Render Pipeline - Pipeline Asset (Forward Renderer)


---
### 3). Project Setting하기
![h:400](./project1/image61.png)
Edit - Project Settings

---

  ![h:400](./project1/image62.png)
  Edit - Project Settings - Graphics(좌측 메뉴바) - Universal Render Pipeline Ass → Scriptable Render Pipeline Settings(여기로 드래그하여 넣기) 
  (Universal Render Pipeline Ass가 안보일 경우 Assets창에서 검색하기(검색 후 제일 왼쪽에 있는 것으로 넣기)Scriptable Render Pipeline Settings은 상단에 위치하고 있음)
    
---

#### Oculus Build하기
  ![h:400](./project1/image63.png)
Oculus - OVR Build - OVR Build APK And Run
하는 이유 : Pc로만 Unity를 재생하기 때문에 실제 VR앱에서 제대로 작동되는 지 확인하기 위함.

---
#### Universal RP 후 오브젝트가 핑크색으로 변할 경우
  ![h:400](./project1/image64.png)
  Edit - Render Pipeline - Universal Render Pipeline - Upgrade Project Materails to UniversalRP Materials
클릭 후 안내창이 뜰 경우 - Proceed(진행)

---

# Unity 오류 발생 시 해결방법 모음
![h:400](./project1/image65.png)

---
#### Console에 해당 오류가 뜬 경우, 또는 Package Manager에서 정상적으로 Import하지 못할 경우
* Package Manager 에서 생긴 오류로 자주 생기는 문제임
 
* 해결방법 : Unity Hub에서 로그아웃 후 재로그인

#### VR기기 착용 후 설정에 오큘러스 링크 연결이 나오지 않을 경우

 * VR 기기의 전원을 끄고 다시 키기
 
 * PC에 있는 오큘러스 앱 계정 로그아웃 후 재로그인
 #### 설정 높이가 너무 높을 경우 VR 영역에서 벗어난 후 다시 높이 설정

 * 높이 설정할 때 컨트롤러를 최대한 바닥에 가깝게 둘 것

 ---
 #### 핸드트래킹이 인식이 잘 안될 때
 * 컨트롤러를 최대한 멀리 둔 후, 뒤집기

 #### 유니티 버전 재설치 후, failed to delete old unity installation files라는 에러가 발생할 때

* C:\Program Files\Unity\Hub\Editor\2019.2.6f1\Editor\Data\PlaybackEngines\ 위에 경로로 가서 AndroidPlayer 폴더 삭제하기 


---

####   유니티 오큘러스 빌드 과정에서 Gradle 오류가 발생했을 때 

![h:400](./project1/image66.png)
Gradle build failed 오류가 발생했을 경우 - 유니티 프로젝트 폴더명과 경로가 한글로 되어 있을 경우 영어로 수정할 것

---

#### 변경 후에도 Gradle build 오류 해결이 안될 경우
- 유니티 종료
- C:\Users\사용자\.gradle\caches 안에 폴더 다 지우기
- C:\Users\nomea\AppData\LocalLow\해당 패키지 이름 폴더째로 삭제
- 재부팅

---

![h:400](./project1/image67.png)

Project Settings - Player - Publishing Settings - Build - Custom Base Gradle Template 체크하기

---

###  Null 오류가 발생했을 때 

![h:400](./project1/image68.png)

---

![h:400](./project1/image69.png)

#### 키코드 설정하기 (보안 강화)
 
* Project Settings - Player - Publishing Settings - Project Keystore - Password 입력(키코드를 이미 보유했을 경우)
* Project Settings - Player - Publishing Settings - Keystore Manager... - 키코드 생성 후 1번 방법으로 하기 (키코드가 없을 경우)


---
![bg left height:4in](./project1/image70.png)
## Unity VR integration 스크립트 사용

Interactable Unity Event Wrapper Script 사용 
(Interactable View에 해당 게임오브젝트(자기 자신)를 드래그 드랍하기)
When Select()
손으로 오브젝트를 집었을 때
When Unselect()
손으로 오브젝트를 놓았을 때
When Interactors Count Updated()
오브젝트가 충돌했을 때

---

## Passthrough

[참고:Youtube](https://youtu.be/9u3QQi6Gnx0)
- edit / projectsetting / player / Other Settings
- color space : linear
- script backend : IL2CPP
- target architectures : ARM64
- minimum API level

---

- OVR camerarig / OVR manager / Quest Features /Experimental
- Experimental Feature enable 체크
- Passthrough capability enable 체크
- insight passthrough / enable passthrough 체크
- 빌드중 OpenXR관련 에러가 발생하여
- oculus / tools / openXR 추가 - restart

---

![h:400](./project1/image71.png)
- passthrough 작동 여부는 oculus link로 확인 불가. 빌드후 해드셋에 업데이트 하여 확인해야함.
- OVRCameraRig에 OVRPassthroughLayer 컴퍼넌트 추가
- OVR passthrough layer / placement : underlay
- window / rendering / lighting / Environment / skybox meterial : none

---
![h:400](./project1/image72.png)
Assets\Oculus\SampleFramework\Usage\Passthrough\Scenes\PassthroughHands.scene

---

# 핸드 트래킹 제스처 작업 가능 리스트
![h:400](./project1/image73.png)
[튜토리얼 영상](https://youtu.be/9u3QQi6Gnx0)

오브젝트 물건을 집는 모션 (21:23~21:30)

---

![h:400](./project1/image74.png)
손을 주먹으로 쥐었다 펴는 동작 (21:09~21:21)


---
![h:400](./project1/image75.png)
오브젝트를 던지는 모션 (21:30~21:31)

---
#### 핸드 트래킹 제스처 작업 가능 리스트

[튜토리얼 영상(2)](https://youtu.be/fZXKGJYri1Y)

![h:400](./project1/image76.png)

* 사물에 닿으면 들고 있는 오브젝트의 변화를 주는 모션 (06:30~06:40)

---

![h:400](./project1/image77.png)

* 장착한 오브젝트(막대기)와 또 다른 오브젝트가 상호작용하는 모션 (06:41~06:45)


---
![h:400](./project1/image78.png)

* 워프를 통해 다른 장소로 이동 하는 기능 (24:01~24:26)


---

#### 핸드 트래킹 제스처 작업 가능 리스트

[튜토리얼 영상(3)]( https://youtu.be/5NRTT8Tbmoc)

![h:400](./project1/image79.png)
* 높은 곳을 손으로 잡고 올라가는 모션 (06:33~06:38)

---

![h:400](./project1/image80.png)
* 중력이 적용되어 높은 곳에 있다가 떨어지는 기능 (11:55~12:02)

---
 
 
#### 핸드 트래킹 제스처 작업 가능 리스트

[튜토리얼 영상(4)](  https://youtu.be/FMu7hKUX3Oo)
![h:400](./project1/image81.png)
* 총을 발사하는 모션 (11:10~11:20)

---


![h:400](./project1/image82.png)
* 오브젝트를 조작할 수 있는 기술 (13:43~14:08)
    오브젝트의 특정 버튼을 클릭할 수 있거나 오브젝트를 자유롭게 던지거나 받을 수 있음


 ---

 #### 핸드 트래킹 제스처 작업 가능 리스트
[튜토리얼 영상(5)](https://youtu.be/4tW7XpAiuDg)
![h:400](./project1/image83.png)
 * UI 기능 조작 기능 (12:17~12:29)
 버튼 클릭 / 옵션 선택 / 버튼 바 조정

 ---
 ![h:400](./project1/image84.png)

 * 오브젝트 선택시 색변화 모션 (18:15~18:23)


 ---
  #### 핸드 트래킹 제스처 작업 가능 리스트
[튜토리얼 영상(6)](https://youtu.be/bYS35_hC6B0)
 ![h:400](./project1/image85.png)
* 문 손잡이를 잡고 열고 닫을 수 있는 모션 (05:06~05:45)

---

 ![h:400](./project1/image86.png)

 * 고정된 막대기를 움직이는 모션 (07:42~07:53)

---

  ![h:400](./project1/image87.png)

  * 사물함 서랍을 열고 닫는 모션 (10:46~11:03)


---

  #### 핸드 트래킹 제스처 작업 가능 리스트

[튜토리얼 영상(7)](https://youtu.be/bYS35_hC6B0)
  ![h:400](./project1/image88.png)
  * 오브젝트(무기)를 드롭할 때 나타나는 모션 (04:29~04:45)

---
  ![h:400](./project1/image89.png)
  * 오브젝트(무기) 인벤토리 기능 (12:19~12:30 / 12:48~12:59 )

---
![h:400](./project1/image90.png)
 * 장신구(모자)를 착용할 수 있는 기능 (08:11~08:17)

---

[튜토리얼 영상(8)](https://youtu.be/mHHYI7hzZ6M)
  ![h:400](./project1/image91.png)
* 벽에 있는 오브젝트를 잡고 올라가는 클라이밍 모션 (10:36~10:55)

---

[튜토리얼 영상(9)]( https://youtu.be/mHHYI7hzZ6M)
![h:400](./project1/image92.png)
- 양손으로 오브젝트를 조정할 수 있는 기능 (20:13~20:42) 


---

[튜토리얼 영상(10)](https://www.youtube.com/watch?v=1FRqniErAfs)
![h:400](./project1/image93.png)
* 실제 손을 인식하여 가상 손이 똑같이 움직이는 기능 (3:17~3:24)

---

![h:400](./project1/image94.png)
* 오브젝트를 집게 손 모양으로 집을 때 상호작용하는 기능 (9:54~10:03)


---

[튜토리얼 영상(11)](https://www.youtube.com/watch?v=P0rbFHWpKnA)
#### 3D 오브젝트 중력 추가와 충돌감지 기능 (01:53~01:59)

* 중력을 통해 오브젝트가 위에서 아래로 떨어짐
* 테이블과 오브젝트가 서로 맞닿았을 때 통과하지 않고 막히는 기능
![bg left height:4in](./project1/image95.png)

---

![bg left height:4in](./project1/image96.png)
![bg left height:4in](./project1/image99.png)
#### 3D 오브젝트 중력 추가와 충돌감지 기능 (01:53~01:59)
* 중력을 통해 오브젝트가 위에서 아래로 떨어짐
* 테이블과 오브젝트가 서로 맞닿았을 때 통과하지 않고 막히는 기능

---
![bg left height:4in](./project1/image100.png)
![bg left height:4in](./project1/image101.png)
오브젝트가 회전축을 중심으로 회전하는 기능 (09:51~09:55)


---
![h:400](./project1/image102.png)

두 손을 사용하여 오브젝트 크기를 확대하거나 축소할 수 있는 기능 (9:46~09:50)

* 양쪽으로 잡아당길 때 : 스케일 확대
* 안쪽으로 손 모을 때 : 스케일 축소

---

[튜토리얼 영상(12)](https://www.youtube.com/watch?v=67hPv3C11Rk)

![h:400](./project1/image103.png)
다양한 손동작으로 컵(오브젝트)을 집는 모션과 기능 (07:12~07:45)
* 여러 개의 손동작을 만들어 오브젝트와 상호작용할 수 있음
* 각도와 손가락 위치 등에 따라 모션이 달라짐

---
![h:400](./project1/image104.png)

컵을 집었을 때 손이 오브젝트와 자동으로 붙는 기능 (09:31~09:35)

---

[튜토리얼 영상(13)](https://www.youtube.com/watch?v=bkn-daQzALQ)

![h:400](./project1/image105.png)

* 핸드트래킹 도중 집게 손을 했을 때, Hand UI의 모양과 색이 변화하는 기능 (07:33~07:41)
* 사용자가 버튼을 조작하거나 오브젝트를 선택해야 할 때, 클릭 또는 상호작용 중이라는 것을 알 수 있게 함

---


![h:400](./project1/image106.png)
* 손이 어떤 오브젝트를 가리키는 지 알 수 있는 기능과 Hand UI 모양 또는 색의 변화 (08:21~08:39)


---
![h:400](./project1/image107.png)

핸드트래킹으로 오브젝트를 상호작용했을 때 색이 변화하는 기능 (08:23~08:36)
 
* 기본 상태(default) : 빨간색 
* 오버(hover) : 파란색
* 클릭 또는 상호작용(click) : 초록색

---

[튜토리얼 영상(14)](https://youtu.be/IDE3eYDadig)

![h:400](./project1/image108.png)

버튼 클릭 기능 (08:45~09:00)
* 버튼 호버 / 버튼을 눌렀을 때 / 버튼을 누르지 않았을 때 각기 색을 다르게 지정하여 오브젝트 행동에 따라 색이 변화함

---
[튜토리얼 영상(15)](https://youtu.be/XOc71-Og0Kg)

![bg left height:4in](./project1/image109.png)





![bg left height:4in](./project1/image110.png)
* 버튼 인터페이스를 통해 UI를 움직이거나 옵션을 설정할 수 있는 기능 (09:54~10:13)

---

[종합적으로 정리한 영상](https://www.youtube.com/watch?v=GF2BswT7EcM&t=249s)

---

# HandTrackingEvent
* 가리키기, 집기, 집기 풀기, 스크롤 및 손바닥 집기
* 1point, pinch, unpinch, scroll, and palm pinch
[상호작용](https://developer.oculus.com/resources/hands-design-interactions/)
OVR Skeleton, OVR Hand


---
# Scene 이동

[참고용 유튜브](https://www.youtube.com/watch?v=JCyJ26cIM0Y)
* DontDestroyOnLoad 관련부분
```` c#
    public static VrSceneManager Instance;
    // Start is called before the first frame update
    private void Awake()
    {​​​​
        Debug.Log(Instance);
        if(Instance != null)
        {​​​​​​​​​​​
            Destroy(Instance.gameObject);
        }​​​​​​​​​​​
        Instance = this;
        DontDestroyOnLoad(Instance.gameObject);
    }​​​​​​​​​​​​​​​​​​
 ````
asyncOperation.allowSceneActivation = false;로 설정되어 있으면.asyncOperation.progress가 0.9에서 멈춘다.

---

[참고용링크](https://m.blog.naver.com/developer_hyw/221043427652)​​​​​​​
Scene 전환시 OVR Camera rig는 각 scene에서 새로 연결 하도록 하고. DonDestroyOnLoad에 올리지 않는다.

---

# VR Avatar 세팅
[유니티링크](https://assetstore.unity.com/packages/tools/game-toolkits/ultimate-character-controller-99962)​​​​​​​

[avatar sdk 다운로드 주소](https://developer.oculus.com/downloads/package/meta-avatars-sdk/)

[avatar sdk 적용방법 유튜브 주소](https://www.youtube.com/watch?v=T7i_HRpG14c)

---

### sdk 적용방법에서 null 파일에 스크립트 적용시 error 메세지
Multiple precompiled assemblies with the same name Newtonsoft.Json.dll included on the current platform. Only one assembly with the same name is allowed per platform. (C:/test/Library/PackageCache/com.unity.nuget.newtonsoft-json@3.0.2/Runtime/Newtonsoft.Json.dll)


---
![bg left height:4in](./project1/image111.png)
스크립트 적용시 뜨는 메세지

---

![h:400](./project1/image112.png)
리다운로드를 위해 파일을 삭제하니까 뜬 창

---
![h:400](./project1/image113.png)
그 외 제공되는 vr프로젝트 play 하는 법, 오큘러스 플랫폼 설치 등
 
스크립트 오류로 진행 어려움


---
# 오류 및 해결내용
 * OnTriggerEnter 이벤트를 위해서는 두 객체 중 하나 이상에 rigged body가 있어야 한다.
   룸스케일시 각 scene의 시작지점을 맞추어야한다. (추가 고려대상)
   world space에서 ui를 띄우다 보니 z위치에 따라 모델링과 관통됨.


---

# 참고 링크

* https://developer.oculus.com/documentation/unity/unity-handtracking/?locale=ko_KR
* http://45.32.49.113/wiki/index.php/%EC%97%B0%EA%B5%AC:_oculus_quest_2_%EC%98%A4%ED%81%98%EB%9F%AC%EC%8A%A4_%ED%80%98%EC%8A%A4%ED%8A%B8_2#passthrough
* https://learn.unity.com/tutorial/unity-hub-mic-unity-editeo-seolci#
* [핸드트래킹 제스쳐](https://youtu.be/vSia7t_WlbQ)



