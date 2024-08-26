해당 내용은 코딩애플🍎 수업을 듣고 정리한 글입니다.   

# 브라우저 호환성을 먼저 맞추자: CSS normalize
브라우저간 통일된 스타일을 주기 위해 특정 스타일을 맨 위에 적고 CSS 코드짜기 시작. 브라우저마다 `<button>`, `<input>`, line-height 등  스타일이 다르므로.   
- [CSS Normalize 링크](https://github.com/necolas/normalize.css/blob/master/normalize.css): 코드를 CSS파일에 복붙하거나, 다운받아서 `<link>` 태그로 첨부

# CSS properties
## Background
- background-color: RGB색상 | rgba(r코드, g코드, b코드, 투명도(0-1사이)) 
- background-size: cover|contain
  - cover: 이미지 배경 짤려도 상관없으니 감싸고있는 공간에 빈 공간없이 배경으로 꽉 채움.
  - contain: 이미지 배경 짤리면 안됨. 감싸고 있는 공간은 남아도 됨.
- background-position: center | right | left
- background-attachment: fixed | scroll
  - scroll: 배경 위치가 고정되어서 스크롤 내리면 배경이 점점 안보임
  - fixed: 스크롤 내려도 배경이 계속 고정
- filter: brightness(70%) | grayscale()
  - brightness: 배경이미지에 밝은 필터 씌어줌. brightness()안의 숫자가 높을수록 밝아짐.
  - 해당 element안에 이미지 말고 글이나 버튼 등 있으면 전부 다 적용 됨.
- background-image: url(url1), url(url2) | linear-gradient | radial-gradient | conic-gradient
  - url(url1), url(url2): 배경 여러개 겹치기 가능, 왼쪽에 있는 이미지가 먼저 나옴. background-size, background-position은 콤마(,)를 이용해 두 배경에 각각 설정
  - linear-gradient(direction, color-stop1, color-stop2, ...) ex) linear-gradient(to right, red , yellow);
  - radial-gradient(shape size at position, start-color, ..., last-color) ex) radial-gradient(red 5%, yellow 15%, green 60%);
  - conic-gradient([from angle] [at position,] color [degree], color [degree], ...) ex) conic-gradient(red, yellow, green, blue, black);
-background-repeat: no-repeat | repeat | space | round;

> [!NOTE]
> <details>
> <summary> margin collapse effect</summary>
>
> ```HTML
> <div class="background">
>   <p class="title" style="margin-top: 50px">글씨</p> 
> </div>
>```
> 위와 같이 `<p>` 태그에 margin-top을 주었을 때 `<div>`와 `<p>` 둘 다 margin-top이 생기는 현상으로 일종의 버그.
> 박스들은 테두리가 만나면 margin이 합쳐짐.  
> 마진을 하나로 합쳐주고, 혹여나 둘 다 마진이 있으면 둘 중에 큰 마진을 하나만 적용하게 됨.   
> => 해결 방법? 두 박스의 테두리가 겹치기 않도록 하면 됨.
> ```HTML
> <!-- 두 박스의 테두리 겹치지 않게 하기 위해서 <div>에 padding-top: 1px 추가 -->
> <div class="background" style="padding-top: 1px">
>   <p class="title" style="margin-top: 50px">글씨</p> 
> </div>
>```
> 
> </details>

## Position
position 속성으로 좌표 지정하기. 공중에 떠 있는 요소.    
position(내 기준점 설정) property 짝꿍 => top/right/left/bottom(움직일 거리) + z-index(누가 위에있냐).   
position 속성을 줬을 때는 꼭 부모를 position:relative 로 감싸는 버릇을 하자! 그래야, css로 위치 계산하기 좋으니깐.       
- position: static | relative | fixed | absolute | sticky
  - static: default 값. 기본 위치.
  - relative: 내 원래 위치 기준. 기준이 내 원래 위치라서 조금씩 옮기기 좋음.
  - absolute: 내 부모 기준(부모가 될 수 있는 조건: 자식부터 상위로 올라가면서 부모 중에 position: relative를 가진 첫번째 부모).
  - fixed: 브라우저 창 기준. 어딘가 고정되는 버튼 만들고 싶을 때. 스크롤 내려도 계속 고정.
  - sticky: 스크롤 기준. 특정 지점에서 멈춤.

### 사용예시   
1) position: relative
  ```HTML
  <head>
    <style>
    .main-button {
      position: relative;
      left: 20px;
    }
    </style>
  </head>

  <body>
    <div class="background" style="padding-top: 1px">
      <p class="title" style="margin-top: 50px">글씨</p> 
      <button class="main-button">구매하기</button>
    </div>
  </body>
  ```
2) position: absolute
  ```HTML
  <head>
    <style>
    .background {
      position: relative;
    }
    .main-button {
      position: absolute;
      button: 20px;
    }
    </style>
  </head>

  <body>
    <div class="background" style="padding-top: 1px">
      <p class="title" style="margin-top: 50px">글씨</p> 
      <button class="main-button">구매하기</button>
    </div>
  </body>
  ```

3) 'position: absolute' 가운데 정렬 => left: 0; right: 0; margin: auto; width: 적당히;
  ```HTML
  <head>
    <style>
    .background {
      position: relative;
    }
    .main-button {
      position: absolute;
      left: 0;
      right: 0;
      margin: auto;
      width: 100px;
    }
    </style>
  </head>

  <body>
    <div class="background" style="padding-top: 1px">
      <p class="title" style="margin-top: 50px">글씨</p> 
      <button class="main-button">구매하기</button>
    </div>
  </body>
  ```

## box-sizing
div 박스의 width를 주게되면, padding, border 고려하지 않고 안쪽 부분만 실제 width로 설정. 근데, 전부 다 합친 사이즈를 width로 주고 싶다면 사용 할 수 있는게 box-sizing   
- box-sizing: border-box | content-box
  - border-box: padding, border 포함해서 width를 설정
  - content-box: default로, padding, border 포함하지 않고 width 설정

### 사용예시
```CSS
div {
  width: 600px;
  box-sizing: border-box;
}
```

## box-shadow
박스에 그림자 주기.
- box-shadow: none|h-offset v-offset blur spread color;
  - none: Default 값. 그림자 없음.
  - h-offset v-offset blur spread color ex) box-shadow: 0.5px 0.5px 2px 1px #eee;

## display: Flex
display 속성으로, 익스플로러 11 이상에서 사용가능.
- display: flex
- flex-direction: row | column
  - row: default 값. 1개의 row로 정렬 => 즉, 가로로 배치
  - column: 1개의 column으로 정렬 => 즉, 아이템을 세로로 배치
- justify-content: center
  - center: 주축을 기준으로 정렬. flex-direction: row => 가로 가운데 정렬, flex-direction: column => 세로 가운데 정렬
- align-items: center | end
  - center: 보조축을 기준으로 정렬. flex-direction: row => 세로 가운데 저렬, flex-direction: column => 세로 가운데 정렬
  - end: 가장 밑단으로 정렬
- flex-wrap: nowrap | wrap 
  - nowrap: defalut 값. 요소들이 자리가 부족할 때 비율로 줄어듬.
  - wrap: 요소의 가로 길이가 크게 되면 최대한 윈도우 사이즈에 맞추고 나머지는 밑으로 내려감
- flex-grow: 숫자
  - 숫자: 박스크기를 비율(숫자배수)로 설정

### 사용예시
```HTML
(flex.html)
<div class="flex-container">
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>
```

```CSS
(flex.css)
.flex-container {
  display : flex;
  flex-direction : column; /* 세로정렬 */
  justify-content : center;  /* 좌우정렬 */
  align-items : center;  /* 상하정렬 */
  flex-wrap : wrap;  /* 폭이 넘치는 요소 wrap 처리 */
}
.box {
  flex-grow : 2;  /* 폭이 상대적으로 몇배인지 결정 */
}
```

## 애니매이션 효과
어떤 스타일 사이를 부드럽게 하기 위해서 주는 효과로, [transition](#transition), [transform](#transform), [Translate](#translate) 세 가지로 활용 가능.

> [!NOTE] 
> <details>
> <summary> 다른 사이트에서 어떤 효과 쓰였는지 확인하는 법 </summary>
>
> 1. 크롬 개발자 도구(F12) > 오른쪽 점세개 메뉴 > More tools > Animations
> 2. 웹사이트에서 애니매이션 실행해봄
> 3. 크롬 개발자의 Animations 탭에서 기록된 애니매이션 클릭
> 4. 어떤 속성이 변했는지 확인
> </details>

### Transition
특정 이벤트(ex. hover <- css에서는 hover이상으로 구현 힘듬. 더 하려면 JavaScript 활용해야 함)가 발생했을 때, 시작 스타일과 최종 스타일 사이의 다른 부분이 부드럽게 전화되기 위해 사용.  

- transition: transition-property, transition-duration, transition-timing-function, transition-delay 를 짧게 축약해 놓은 버전   
  ex1) transition: all 2s   
  ex2) transition: width .35s ease-in-out;   
- transition-property: none|all|property|initial|inherit;
  - none: 트랜잭션 효과 없음.
  - all: default 값. 모든 property가 트랜잭션 효과 있음.
  - property: 트랜잭션을 주고 싶은 css propery 이름을 ','로 구분하여 작성 ex) transition-property: width, height;
- transition-duration: time|initial|inherit;
  - time: 효과를 몇 초 동안 할 것인지 작성 ex) 3s 
- transition-timing-function: linear|ease|ease-in|ease-out|ease-in-out|step-start|step-end|steps(int,start|end)|cubic-bezier(n,n,n,n)|initial|inherit;
- transition-delay: time|initial|inherit;
  - time: 몇 초 뒤에 효과가 실행될 것인지 작성 ex) 2s
> [!NOTE]
> <details>
> <summary>애니메이셔 만드는 순서</summary>
> 
> Step 1. 시작 스타일, 최종 스타일 만들기   
> Step 2. 언제 최종 스타일로 변하는지 결정해주기 ex) 마우스를 올렸을 때(:hover)   
> Step 3. transition 으로 애니매이션 만들기   
> *주의사항: 스타일의 selector와 최종 스타일의 selector 는 "언제" 만을 제외하곤 동일해야 함. 
> ex) 시작스타일: .overlay 최종스타일: .overlay (O)   
> ex) 시작스타일: div.overlay 최종스타일: .overlay (X)
> ```CSS
> /* Step 1. 시작 스타일*/
> .overlay {
>   background-color: rgba(0, 0, 0, 0.5);
>   opacity: 0;
>   transition: all 1s; /* Step 3. 어떻게 변하는지 => 주의!!! 최종 스타일이 아닌 시작 스타일에 넣기 */
> }
>  + 
> .overlay:hover {      /* Step 2. 언제 변하는지 */
>   opacity: 1;         /* Step 1. 최종 스타일 */
> }
> ```
> </details>

### Transform
특정 요소를 회전하거나 사이즈 변경 등 형태 변화를 할 때 사용.   
- transform: none|transform-functions|initial|inherit;
  - transform-functions: [참고링크](https://www.w3schools.com/cssref/playdemo.php?filename=playcss_transform&preval=none) ex) transform: rotate(20deg);


### Translate
특정 요소의 위치를 변경할 때 사용. [참고링크](https://www.w3schools.com/cssref/css_pr_translate.php)
- translate: x-axis y-axis z-axis|initial|inherit;




## Font
### 사용예시
- 기본 사용
```CSS
body {
  font-family : 'gulim', 'gothic'
}
```
- 외부 폰트 다운로드 해서 등록하여 사용
```CSS
/* 외부 폰트 다운로드해서 등록*/
@font-face{ 
  font-family: 'Lato';
  src:url(/font/Lato.ttf) format("truetype"); /* url(폰트경로) format(포맷)*/
  font-style:normal;
  font-weight:normal; 
}

/* 사용 */
body {
  font-family: 'Lato';
}  
```
> [!NOTE] 
> 한글폰트 ttf 파일은 용량이 매우 크기 때문에 1-2개만 쓰자 => 구할 수 있다면, 웹 폰트용으로 나온 woff을 쓰자. ttf에 비해 용량이 3분의1 수준임.

### 폰트를 빠르게 사용하기 위한 Google Fonts
- [Google Fonts](https://fonts.google.com/?preview.layout=grid)
  ```HTML
  (fontTest.html)
  <head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap" rel="stylesheet">
  </head>
  ```
  ```CSS
  (fontTest.css)
  .roboto-regular {
    font-family: "Roboto", sans-serif;
    font-weight: 400;
    font-style: normal;
  }
  ```

> [!NOTE]
> <details>
> <summary>폰트 Anti-aliasing</summary>
>
> 가끔 웹폰트가 깨진것 처럼 보일 때가 있음. 이걸 수정하기 위한게 anti aliasing인데, 폰트가 깨져있는 부분을 부드럽게 바꿔주는 것.
> CSS 파일에다가 transform()을 써서 글자를 살짝 돌려주면 anti aliasing 효과 낼 수 있음.
> ```CSS
> p, div {
>   transform : rotate(0.04deg); 
> }
>```
> </details>


# CSS Selector
- [CSS Selector 참고](https://www.w3schools.com/cssref/css_selectors.php)

| Selector                 | Example                    | Example Description                                                                 |
|--------------------------|----------------------------|-------------------------------------------------------------------------------------|
| `.class`                 | `.intro`                   | 클래스 이름이 `intro` 인 모든 요소 선택                    |
| `.class1.class2`         | `.name1.name2`             | 클래스 이름이 `name1`, `name2` 둘 다 갖는 모든 요소 선택   |
| `.class1 .class2`        | `.name1 .name2`            | 클래스 이름이 `name2` 인 모든 요소를 선택하는데, 부모의 클래스 이름이 `name1`인 것    |
| `#id`                    | `#firstname`               | 아이디 이름이 `firstname`인 모든 요소 선택                 |
| `*`                      | `*`                        | 모든 요소 선택                                            |
| `element`                | `p`                        | 모든 `<p>` 요소 선택                                      |
| `element.class`          | `p.intro`                  | `<p>` 요소 중 클래스 이름이 `intro` 인 것 선택             |
| `element,element`        | `div, p`                   | 모든 `<div>` 요소와 모든 `<p>` 요소 선택                   |
| `element element`        | `div p`                    | 모든 `<p>` 요소 선택하는데, 부모가 `<div>` 인 것            |
| `element>element`        | `div > p`                  | `<div>` 의 바로 아래에 있는 모든 `<p>` 태그 선택            |
| `element+element`        | `div + p`                  | `<div>` 의 형제 중 첫번째 `<p>` 요소만 선택          |
| `element1~element2`      | `p ~ ul`                   | Selects every `<ul>` element that is preceded by a `<p>` element                    |
| `[attribute]`            | `[target]`                 | Selects all elements with a `target` attribute                                      |
| `[attribute=value]`      | `[target="_blank"]`        | Selects all elements with `target="_blank"`                                         |
| `[attribute~=value]`     | `[title~="flower"]`        | Selects all elements with a `title` attribute containing the word "flower"          |
| `[attribute\|=value]`    | `[lang\|="en"]`            | Selects all elements with a `lang` attribute value equal to `"en"` or starting with `"en-"` |
| `[attribute^=value]`     | `a[href^="https"]`         | Selects every `<a>` element whose `href` attribute value begins with `"https"`      |
| `[attribute$=value]`     | `a[href$=".pdf"]`          | Selects every `<a>` element whose `href` attribute value ends with `".pdf"`         |
| `[attribute*=value]`     | `a[href*="w3schools"]`     | Selects every `<a>` element whose `href` attribute value contains the substring `"w3schools"` |
| `:active`                | `a:active`                 | Selects the active link                                                             |
| `::after`                | `p::after`                 | Insert something after the content of each `<p>` element                            |
| `::before`               | `p::before`                | Insert something before the content of each `<p>` element                           |
| `:checked`               | `input:checked`            | Selects every checked `<input>` element                                             |
| `:default`               | `input:default`            | Selects the default `<input>` element                                               |
| `:disabled`              | `input:disabled`           | Selects every disabled `<input>` element                                            |
| `:empty`                 | `p:empty`                  | Selects every `<p>` element that has no children (including text nodes)             |
| `:enabled`               | `input:enabled`            | Selects every enabled `<input>` element                                             |
| `:first-child`           | `p:first-child`            | Selects every `<p>` element that is the first child of its parent                   |
| `::first-letter`         | `p::first-letter`          | Selects the first letter of every `<p>` element                                     |
| `::first-line`           | `p::first-line`            | Selects the first line of every `<p>` element                                       |
| `:first-of-type`         | `p:first-of-type`          | Selects every `<p>` element that is the first `<p>` element of its parent           |
| `:focus`                 | `input:focus`              | Selects the input element that has focus                                            |
| `:fullscreen`            | `:fullscreen`              | Selects the element that is in full-screen mode                                     |
| `:has()`                 | `h2:has(+p)`               | Selects `<h2>` elements that are immediately followed by a `<p>` element            |
| `:hover`                 | `a:hover`                  | Selects links on mouse over                                                         |
| `:in-range`              | `input:in-range`           | Selects input elements with a value within a specified range                        |
| `:indeterminate`         | `input:indeterminate`      | Selects input elements that are in an indeterminate state                           |
| `:invalid`               | `input:invalid`            | Selects all input elements with an invalid value                                    |
| `:lang()`                | `p:lang(it)`               | Selects every `<p>` element with a `lang` attribute equal to `"it"` (Italian)       |
| `:last-child`            | `p:last-child`             | Selects every `<p>` element that is the last child of its parent                    |
| `:last-of-type`          | `p:last-of-type`           | Selects every `<p>` element that is the last `<p>` element of its parent            |
| `:link`                  | `a:link`                   | Selects all unvisited links                                                         |
| `::marker`               | `::marker`                 | Selects the markers of list items                                                   |
| `:not()`                 | `:not(p)`                  | Selects every element that is not a `<p>` element                                   |
| `:nth-child()`           | `p:nth-child(2)`           | Selects every `<p>` element that is the second child of its parent                  |
| `:nth-last-child()`      | `p:nth-last-child(2)`      | Selects every `<p>` element that is the second child of its parent, counting from the last child |
| `:nth-last-of-type()`    | `p:nth-last-of-type(2)`    | Selects every `<p>` element that is the second `<p>` element of its parent, counting from the last child |
| `:nth-of-type()`         | `p:nth-of-type(2)`         | Selects every `<p>` element that is the second `<p>` element of its parent          |
| `:only-of-type`          | `p:only-of-type`           | Selects every `<p>` element that is the only `<p>` element of its parent            |
| `:only-child`            | `p:only-child`             | Selects every `<p>` element that is the only child of its parent                    |
| `:optional`              | `input:optional`           | Selects input elements with no `"required"` attribute                               |
| `:out-of-range`          | `input:out-of-range`       | Selects input elements with a value outside a specified range                       |
| `::placeholder`          | `input::placeholder`       | Selects input elements with the `"placeholder"` attribute specified                 |
| `:read-only`             | `input:read-only`          | Selects input elements with the `"readonly"` attribute specified                    |
| `:read-write`            | `input:read-write`         | Selects input elements with the `"readonly"` attribute NOT specified                |
| `:required`              | `input:required`           | Selects input elements with the `"required"` attribute specified                    |
| `:root`                  | `:root`                    | Selects the document's root element                                                 |
| `::selection`            | `::selection`              | Selects the portion of an element that is selected by a user                        |
| `:target`                | `#news:target`             | Selects the current active `#news` element (clicked on a URL containing that anchor name) |
| `:valid`                 | `input:valid`              | Selects all input elements with a valid value                                       |
| `:visited`               | `a:visited`                | 방문했던 적이 있는 모든 a링크 |





## CSS pseudo-class(:)
상태에 따라서 스타일을 줄 수 있음. hover, focus, active 스타일 넣을 때 순서는 꼭 이걸로 지켜야 함.   
- .btn:hover  => 마우스를 올려놓을 때
- .btn:focus  => 클릭 후 계속 포커스 상태일 때
- .btn:active => 클릭 중일 때

# CSS 단위
- px: 픽셀
- %: 퍼센트
- vw: 현재 브라우저 폭에 비례
- vh: 현재 브라우저 높이에 비례
- rem: 상대적인 단위. html 태그 폰트 사이즈(default: 16px)의 10배. 요즘은 거의 안씀.
- em: 내 폰트 사이즈의 x배

# Responsive Web
디바이스 사이즈에 맞춰서 웹 페이지 개발

## 설정
`<head>` 에 아래 코드 추가하고 시작
```HTML
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

## Media query
CSS 파일 최하단에 적음. Bootstrap [responsive breakpoints](https://getbootstrap.com/docs/4.1/layout/overview/#responsive-breakpoints) 참고

- Breakpoint 참고: 4개 다 쓰기 복잡하다면, 1200px 이하는 태블릿, 768px 이하는 모바일 이렇게 디자인하는게 가장 간편.
  ```CSS
  // Large devices (desktops, less than 1200px)
  @media screen and (max-width: 1200px) { ... }

  // Medium devices (tablets, less than 992px)
  @media screen and (max-width: 992px) { ... }

  // Small devices (landscape phones, less than 768px)
  @media screen and (max-width : 768px) { ... }

  // Extra small devices (portrait phones, less than 576px)
  @media screen and (max-width: 576px) { ... }
  ```


# HTML `<head>`태그
HTML `<head>`태그 안에 들어가는 내용 정리

## 각종 CSS 파일들
```HTML
<head>
  <link href="css/main.css" rel="stylesheet">
</head>
```

## 사이트 제목
```HTML
<head>
  <title>네이버입니다</title>
</head>
```

## meta 태그
마케팅, SEO를 위해서는 meta 태그 중요
- charset: 인코딩 형식
- name="description": 검색엔진에서 뜨는 설명글
- meta name="keywords": 검색에 도움을 주는 키워드
- name="viewport"
  - width=device-width는 모바일 기기의 실제 폭으로 렌더링
  - initial-scale=1: 접속 시의 화면 줌레벨 설정
```HTML
<head>
  <meta charset="UTF-8">
  <meta name="description" content="검색엔진에서 뜨는 설명글">
  <meta name="keywords" content="검색에 도움을 줄 수 있는 키워드">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

## open graph
페이스북, 트위터, 네이버 등. 링크 공유했을 때 링크 관련하여 뜨는 정보. og:, twitter: 등 소셜 페이지 직접 들어가서 참고하여 작성하면 됨.
```HTML
<head>
  <meta property="og:image" content="/이미지경로.jpg">
  <meta property="og:description" content="사이트설명">
  <meta property="og:title" content="사이트제목">
</head>
```

## Favicon
웹사이트 제목 옆에 뜨는 아이콘으로 .ico가 호환성은 가장 좋고 사이즈는  32 x 32.   
웹사이트를 바탕화면에 바로가기 추가했을 경우 뜨는 아이콘도 커스터마이징 가능 => rel="apple-touch-icon-precomposed" 
```HTML
<head>
  <link rel="icon" href="아이콘경로.ico" type="image/x-icon">
</head> 
```

# CSS overwriting
1. 같은 클래스명이나 스타일을 하단에 작성 => CSS 파일은 같은 clsss 라도 하단에 정의한 스타일 우선 적용  
2. id, style 등 우선순위를 높여 작성 => `tag < class < id < style=""(HTML파일) < !important` 순으로 우선순위가 높음.
3. Specificity (구체성 점수) 높여서 작성 => 셀렉터를 여러개 나열하여서 점수 높임.

> [!NOTE]그래서 CSS 파일 사용할 때, div.container  div.box 이런 식으로 길게 복잡하게 쓰면 나중에 덮어쓰기가 힘듬 => 나중에 덮어쓰기할 상황을 생각하면 class 이름은 하나만 써서 작성하는게 좋은 방법.


# OOCSS, BEM: class 작명법
## Object Oriented CSS (OOCSS)
뼈대용 class, 살점용 class 각각 제작.

### 사용예시
1. 버튼
버튼을 만든다고 하면 '버튼의 공통적인 부분을 갖는 class  + 특징을 담고 있는 classes'를 만들자.  
  ```CSS
  .main-btn{
    padding : 15px;
    border : none;
    cursor : pointer;
  }
  .bg-red {
    background: red;
  }
  .bg-blue {
    background: blue;
  }
  ```
2. Utility class
Bootstrap에서 사용하는 방식임.
  ```CSS
  .font-small {
    font-size : 12px;
  }
  .font-medium {
    font-size : 16px;
  }
  .font-lg {
    font-size : 20px;
  }
  ```

## Block__Element--Modifier (BEM)
class 작명할 떄 클래스명 중복되지 않고 쉽게 작명하도록 도와줌. 근데 무조건 지킬 필요는 없고, 비슷하게만 차용하는게 좋을듯.    
=> 현재는 다른 JavaScript library가 많아지면서 html페이지 단위가 아닌 UI 단위로 개발하면서 클래스명 중복 확률도 줄어들었고, BEM 지켜서 작명하면 너무 길어지거나 OOCSS 못쓸 수도 있으니.

### 사용예시
```HTML
<div class="profile">
  <img class="profile__img">
  <h4 class="profile__h4">이름</h4>
  <p class="profile__content">소개글</p>
  <button class="profile__button--red">빨간버튼</button>
  <button class="profile__button--blue">파란버튼</button>
</div>
```

# Bootstrap (v5.0)
Component Library. 기본적인 요소들을 이쁘게 디자인하여 모아놓은 라이브러리. 

## 사용법
[Bootstrap 참고](https://getbootstrap.com/docs/5.0/getting-started/introduction/)

## 자주쓰는 기능
### Layout
- [Container](https://getbootstrap.com/docs/5.0/layout/containers/)
- [Grid (row/col)](https://getbootstrap.com/docs/5.0/layout/grid/)

### Forms
- [Form](https://getbootstrap.com/docs/5.0/forms/form-control/)


### Component
- [Card](https://getbootstrap.com/docs/5.0/components/card/)
- [Modal](https://getbootstrap.com/docs/5.0/components/modal/)
- [Navbar](https://getbootstrap.com/docs/5.0/components/navbar/)

### Utility
- [API](https://getbootstrap.com/docs/5.0/utilities/api/)


# 유용한 부가기능 (VS Code용)
## 코드 정렬
- 우클릭 > Format Document

## Emmet
셀렉터 이용해서 HTML을 좀 더 쉽게 생성할 수 있는 부가기능. VS code는 기본으로 설치되어 있음. 

### 사용예시
- HTML 기본 양식 자동 완성: ! + tab키
- 임시글자 무작위 생성: lorem + tab키
- div.container>div + tab키
  ```HTML
  <div class="container">
    <div></div>
  </div>
  ```
- div#header>p.title*3 + tab키
  ```HTML
  <div id="header">
    <p class="title"></p>
    <p class="title"></p>
    <p class="title"></p>
  </div>
  ```
- CSS
  ```CSS
  margin : 10px     /* m10 + tab키 */
  margin-top : 10px /* mt10  + tab키 */
  width : 100%      /* w100% + tab키 */
  ```

# 디버깅
- 크롬 개발자 도구(F12) 이용
