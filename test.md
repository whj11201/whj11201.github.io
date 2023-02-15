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

적용안됨
```css
style: |
 .columns {
    display: grid;
    grid-template-colums: repeat(2, minmax(0, 1fr));
    gap: 1rem;
 }
```
적용됨
```css
 style: |
    .columns {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 1rem;
    }
```
---
 ## 
* grid-template-columns를 colums로 입력하여 인식이 안되 적용이 실패함

---
### 고치난 후 정상 작동

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