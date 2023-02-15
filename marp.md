---
marp: true
theme: uncover
class: invert
paginate: true
header: Marp tutorial
footer: 2023-02-13
style: |
    .columns {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 1rem;
    }
---
<!--_color: skyblue-->
 # Marp Tutorial 과정


 ---
# Code


```thml

{```python
def add(a, b):
  """A super helpful function!"""
  return a + b
  ```}

```

```python
def add(a, b):
  """A super helpful function!"""
  return a + b
  ```


  ---

  # Math
 ```thml

 한줄 표현
$\mathcal{0}(n\log{n})$

다중 표현

$$
\begin{align}
 x &= 1 + \frac{1}{2}\\
   &= 1.5
   \end{align}
   $$
```

---

###### 예시
한줄 표현
$\mathcal{0}(n\log{n})$

다중 표현

$$
\begin{align}
 x &= 1 + \frac{1}{2}\\
   &= 1.5
   \end{align}
   $$


 ---
 ### 이미지 좌측 설정 및 추가목록(부가설명)

 ```thml
![bg left height:4in](./폴더이름/이미지.png)

 *1
 *2


 ```
---
 ###### 이미지 좌측 설정 및 추가목록
 ![bg left height:4in](./marpimg/image.png)

 *1
 *2

---
## Color 추가
```thml
 <!--_color: red-->
      폰드색상
 <!--_backgroundColor: black-->
      배경 색상
 # 넣고싶은 문구
```
---
### 예시
 <!--_color: SKYBLUE-->
 <!--_backgroundColor: purple-->


 ---

 ## 텍스트 좌우 배치
![h:400](./marpimg/image2.png)
설정-설정-enable html검색 확인-체크

---
````html
style: |
    .columns {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 1rem;
    ---

 <div class="columns">
 <div>

 * a
 * b
 * c
 </div>

 <div>

 * d
 * e
 * f
 </div>
 </div>


 ---
 }


````

---
### 예시
 <div class="columns">
 <div>

 * a
 * b
 * c
 </div>

 <div>

 * d
 * e
 * f
 </div>
 </div>


 ---

### 적용이 잘 안된 사유
"https://github.com/whj11201/whj11201.github.io/blob/main/test.md"

 ---
 
## PDF로 생성

show Quick pick of Marp Commands
(겹 쳐있는 직각삼각형모양) 

클릭후 Export Slide DECK 클릭 후 
자기가 원하는 파일 위로 export를 눌러 생성
  