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

**_파일명.scss 연결 css 자동 업데이트**

파일구조
- _test.scss
- main.scss -> test.scss import
- main.css -> _test.scss가 업데이트 되면 자동으로 업데이트 되어야하는데 vscode에서는 지원하지 않음.
- main.css.map

"_파일명.scss" 파일이 저장됐을 때, 이 파일이 import 되어있는 scss가 자동으로 업데이트 되어 컴파일 하는 것을 원했는데(phpstorm ruby 자동 업데이트 컴파일 방식) vscode 에디터에서는 지원하지 않음. import 되어있는 scss 파일에서 다시 업데이트 시켜줘야 관련 css, map 파일이 업데이트 됨.

**결론 : 위 에러가 뜨고 vscode에서는 import된 파일 자동 업데이트 기능 지원하지 않음..**

<br>

`"liveSassCompile.settings.forceBaseDirectory": "${workspaceFolder}/${relativeFileDirname}"` 

이 부분은 그대로 사용, 이 부분을 지우면 "_파일명.scss" 파일 저장시 작업 영역에 있는 모든 scss가 컴파일 된다.
* 각 SCSS 파일의 컴파일 범위를 해당 파일이 위치한 디렉토리로 제한, 따라서 프로젝트 전체가 아닌, 현재 작업 중인 SCSS 파일과 관련된 CSS 파일만 업데이트


참고 사이트

https://github.com/ritwickdey/vscode-live-sass-compiler/blob/master/docs/settings.md

<br>

---
### __phpstorm scss 세팅__

![세팅1](https://github.com/1GYOU1/SCSS/assets/90018379/5f49dd1e-ec6f-47c1-9b04-914c380bb274)

![세팅2](https://github.com/1GYOU1/SCSS/assets/90018379/c0d08c15-06e5-4ad3-92f9-6b9ddc29424e)

![세팅3](https://github.com/1GYOU1/SCSS/assets/90018379/c5fe99a7-db1c-4c9f-beea-c56bd2b188cd)

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