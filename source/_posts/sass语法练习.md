---
title: sass语法练习
date: 2021-09-24 09:45:55
tags:
---
## @extend | 选择器 | & | mixin
- **@extend**
```css
.error {
  border: 1px #f00;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
```
将error的样式继承给seriousError

- **选择器**
选择器>、+和~
```css
header > p { font-size: 1.1em }
```
选择article 后面紧跟着的子元素中的section元素
```css
header + p { font-size: 1.1em }
```
选择header  后面紧跟的p元素
```css
header ~ p { font-size: 1.1em }
```
选择header  同一层的p元素
- **&**
```css
#main {
  $width: 5em !global;
  width: $width;
}

#sidebar {
  width: $width;
}
```
变量&开头, ！global可将块级作用域变为全局左作用域
```css
p:before {
  content: "I ate #{5 + 10} pies!";
}

p {
  $font-size: 12px;
  $line-height: 30px;
  font: #{$font-size}/#{$line-height};
}
```
#{}为动态变量
- **mixin**
```css
//$point 是参数
@mixin breakpoint($point){
    @media only screen and (max-width: $point) {
        @content;
    }
}

@mixin point-sm{
    @include breakpoint($breakpoint-sm){
        //此处可加其他自定义样式代码
        @content;    
    }
}

@mixin point-md{
    @include breakpoint($breakpoint-md){
        @content;    
    }
}

@mixin point-lg{
    @include breakpoint($breakpoint-lg){
        @content;    
    }
}

@mixin point-xlg{
    @include breakpoint($breakpoint-xlg){
        @content;    
    }
}

/*
.demo{
    @include point-sm{
        background: #ccc;
    }
}
 */
```

