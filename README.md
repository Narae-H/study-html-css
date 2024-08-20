오랜만에 정리해보는 CSS

> [!NOTE] VS Code에서 HTML 기본 양식 자동완성 방법: ! + Tab

# Background
### 사용법
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

# Position
position 속성으로 좌표 지정하기. 공중에 떠 있는 요소. position(내 기준점 설정) + top/right/left/bottom 같이 써야함.
### 사용법
- position: relative | fixed | static
  - relative: 기준이 내 원래 위치.
  - static: 기준이 없음. 좌표적용 불가.
  - fixed: 기준이 브라우저 창. 어딘가 고정되는 버튼 만들고 싶을 때.
  - absolute: 기준이 내 부모.(가장 가까운 부모 중에 position: relative를 가진 부모)
   
- position: relative
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
- position: absolute
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

- 'position: absolute' 가운데 정렬=> left: 0; right: 0; margin: auto; width: 적당히;
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