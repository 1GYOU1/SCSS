## __SCSS__

----

<br>

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