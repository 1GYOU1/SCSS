## __SCSS__
----

### __vscode scss 세팅__
1. Sass(.sass only), Live Sass Compiler, node.js 설치
2. ctrl + , => settings.json 검색
3. 하단 코드 복사 붙여넣기.

```js
{
  "liveServer.settings.CustomBrowser": "chrome",
  "liveSassCompile.settings.autoCompile": false,
  "liveSassCompile.settings.forceBaseDirectory": "${workspaceFolder}/${relativeFileDirname}",
  "liveSassCompile.settings.formats": [
    {
      "format": "expanded",
      "extensionName": ".css",
      "savePath": "~/",
                  //  "~/../css/"
    },
    {
      "format": "compressed",
      "extensionName": ".min.css",
      "savePath": "~/",
                  //  "~/../css/"
    }
  ],
  "liveSassCompile.settings.generateMap": true,
  "liveSassCompile.settings.excludeList": ["**/node_modules/**", ".vscode/**"],
  "json.format.enable": false,
  "liveSassCompile.settings.extraSCSSWatchers": [
    {
      "match": "**/_*.scss",
      "doNotCompile": false
    }
  ],
  "json.schemas": [
  ]
}
```

> Error with your `forceBaseDirectory` setting
Can not find path: d:\바탕화면-d\1gyou1\${workspaceFolder}\${relativeFileDirname}
Setting: "${workspaceFolder}/${relativeFileDirname}"
Workspace folder: 1gyou1

내가 원한건 "_어쩌구.scss" 파일이 저장됐을 때, 이 파일이 import 되어있는 scss를 컴파일 하는 건데...(phpstorm ruby 사용 방식..)

위 에러가 뜨고 vscode에서는 애초에 이런 방식을 지원하지 않았다...

그러나 "_어쩌구.scss" 파일 저장했을 때 작업영역 전체의 scss파일이 컴파일되지는 않아서 
`"liveSassCompile.settings.forceBaseDirectory": "${workspaceFolder}/${relativeFileDirname}"` 

이 부분은 그대로 사용하기로... 이걸 지우면 "_어쩌구.scss" 파일 저장시 작업 영역에 있는 모든 scss가 컴파일 됌 ㅠ

참고 사이트

https://github.com/ritwickdey/vscode-live-sass-compiler/blob/master/docs/settings.md

<br>

---

[@for 문 사용](https://abcdqbbq.tistory.com/83)

[@for 문 each 사용](https://hyeyeong1011.github.io/2020-02-19-post19/)

<br>

### __@mixin 사용__

<br>

선언
```scss
@mixin abc {
    100% {
        visibility: hidden;
    }
}
```
<br>

include해서 사용
```scss
@keyframes showHide {
    0% {
        visibility: visible;
    }
    @include abc;
}
```
<br>

### __@mixin + @if 조건문 사용__
<br>

예시1)
```scss
@mixin pink($type) {
	@if $type == color{
		color:pink;
	}
	@else if $type == bg{
		background-color:pink;
	}
}
```
```scss
@include pink(color);
@include pink(bg);
```
<br>

예시2)
```scss
@mixin fontSize($size) {
	@if $size == small{
		font-size:12px;
	}
	@else if $size == midium{
		font-size:16px;
	}
  @else if $size == big{
		font-size:24px;
	}
}
```
```scss
@include fontSize(small);
@include fontSize(midium);
@include fontSize(big);
```

<br>

----

<br>

### __Interpolation(보간법) 사용__

<br>

```scss
/* 변수 */
$page: main;

/* SCSS 적용 (O) */
.#{$page}_wrap{
  ...
}
```

[Interpolation 보간법](https://abcdqbbq.tistory.com/82)

<br>

----

<br>

### __@for문 from to__

<br>

to 뒤에 나오는 숫자 <b>미만</b>으로 반복되는 값 사용

<br>

SCSS ↓↓
```scss
@for $i from 0 to 5{
  .abc_{$i}{
    background-position:0 ($i * -10px);
  }
}
```
CSS ↓↓
```css
.abc_0{background-position:0 0;}
.abc_1{background-position:0 -10px;}
.abc_2{background-position:0 -20px;}
.abc_3{background-position:0 -30px;}
.abc_4{background-position:0 -40px;}
```
<br>

### __@for문 from through__

<br>

through 뒤에 나오는 숫자 <b>이하</b>로 반복되는 값 사용

<br>

SCSS ↓↓
```scss
@for $i from 0 through 5{
  .abc_#{$i}{
    background-position:0 ($i * -10px);
  }
}
```
CSS ↓↓
```css
.abc_0{background-position:0 0;}
.abc_1{background-position:0 -10px;}
.abc_2{background-position:0 -20px;}
.abc_3{background-position:0 -30px;}
.abc_4{background-position:0 -40px;}
.abc_5{background-position:0 -50px;}
```

<br>

----

<br>

### __@each list 데이터 반복__

<br>

SCSS ↓↓

```scss
@each $변수 in 데이터 {
  실행문
}
```

SCSS ↓↓
```scss
$colors: (red, orange, yellow ,green);

.colors {
    @each $img_name in $colors {
        li.#{$img_name} {
            background: url(img/#{$img_name}.svg);
        }    
    }
}
```

CSS ↓↓
```css
.colors li.red {
  background: url(img/red.svg);
}

.colors li.orange {
  background: url(img/orange.svg);
}

.colors li.yellow {
  background: url(img/yellow.svg);
}

.colors li.green {
  background: url(img/green.svg);
}
```
<br>

### __@each map 데이터 반복__

<br>

SCSS ↓↓
```scss
@each $key변수, $value변수 in 데이터 {
  실행문
}
```

SCSS ↓↓
```scss
$colors-data: (
    red: first,
    orange: second,
    yellow: third,
    green: fourth
);

@each $color, $order in $colors-data {
    .colors {
        li.color-#{$color} {
            background: url(img/#{$order}.svg);
        }
    }
}
```
map 데이터를 반복 할 때는 하나의 데이터에 두개의 변수가 필요

<br>

CSS ↓↓
```css
.colors li.color-red {
  background: url(img/first.svg);
}

.colors li.color-orange {
  background: url(img/second.svg);
}

.colors li.color-yellow {
  background: url(img/third.svg);
}

.colors li.color-green {
  background: url(img/fourth.svg);
}
```