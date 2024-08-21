해당 내용은 코딩애플🍎 수업을 듣고 정리한 글입니다.   

# 브라우저 호환성을 먼저 맞추자: CSS normalize
브라우저간 통일된 스타일을 주기 위해 특정 스타일을 맨 위에 적고 CSS 코드짜기 시작. 브라우저마다 `<button>`, `<input>`, line-height 등  스타일이 다르므로.   
- [CSS Normalize 링크](https://github.com/necolas/normalize.css/blob/master/normalize.css): 코드를 CSS파일에 복붙하거나, 다운받아서 `<link>` 태그로 첨부

# CSS properties
## Background
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
- background-image: url(url1), url(url2)
  - 배경 여러개 겹치기 가능, 왼쪽에 있는 이미지가 먼저 나옴
  - background-size, background-position은 콤마(,)를 이용해 두 배경에 각각 설정

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
position 속성으로 좌표 지정하기. 공중에 떠 있는 요소. position(내 기준점 설정) + top/right/left/bottom 같이 써야함.   
- position: relative | fixed | static
  - relative: 기준이 내 원래 위치.
  - static: 기준이 없음. 좌표적용 불가.
  - fixed: 기준이 브라우저 창. 어딘가 고정되는 버튼 만들고 싶을 때.
  - absolute: 기준이 내 부모.(가장 가까운 부모 중에 position: relative를 가진 부모)

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

## Flex
display 속성으로, 익스플로러 11 이상에서 사용가능.
- display: flex
- flex-direction: column | row
  - column: 세로정렬
  - row: 가로정렬
- justify-content: center
  - center: 가로 가운데 정렬
- align-items: center | end
  - center: 세로 가운데 정렬
  - end: 가장 밑단으로 정렬
- flex-wrap: wrap
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


# CSS pseudo-class(:)
상태에 따라서 스타일을 줄 수 있음. hover, focus, active 스타일 넣을 때 순서는 꼭 이걸로 지켜야 함.   
- .btn:hover  => 마우스를 올려놓을 때
- .btn:focus  => 클릭 후 계속 포커스 상태일 때
- .btn:active => 클릭 중일 때

# HTML head태그


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

