# CSS 样式

CSS : Cascade Style Sheet, 层次样式表. 国内的人都喜欢叫CSS. 它决定了网页的样子.

## 使用方法

- 外部使用:

```html
<head>
  <link href="/assets/application.css" media="screen" rel="stylesheet" type="text/css" />
</head>
```

- 网页内部使用
```html
<style>
.red_box {
  border: 1px solid red;
}
</style>
```

- 行内使用(inline style)
```html
<div style='border: 1px solid red'></div>
```

## &lt;style>中的css 的定义方式(css selector)

有不同的定义方式: 根据id , 根据 class, 根据标签名字, inline声明

```html
<style>
div{
  background-color: yellow;
}
.my_class {
  border: 3px solid red;
}
#my_id {
  color: green;
}
</style>
<div class='my_class' id='my_id' style='font-size: 30px'>
  hello, world!
</div>

```

看起来的样子是:

![例子](http://image.happysoft.cc/image/11/style_demo.jpg)

## CSS Selector (选择器)

我如何精确为某个div加样式, 其他元素不加样式呢? 例如:

```html
<div class='parent'>
  <div class='red big'>
    第一个div
  </div>
  <div class='red'>
    第二个div
  </div>
  <div class='blue'>
    第三个div
  </div>
</div>
<div class='big'>
    第四个div
</div>
```

如果要为 第一个div 增加样式, 又不会影响到第四个div, 就可以:

```css
div.parent div.big{ color: red }
```
也可以简写成:
```css
.parent .big{ color: red }
```

## Selector的权重:
这个文章很好:
https://css-tricks.com/specifics-on-css-specificity/

```html
<div class='parent'>
  <div id='first_id' class='first_class'>
    <p class='red'>第一个div</p>
  </div>
</div>
```

如果我让p 的颜色是红色,有下面若干声明方式:

```css
p             { color: red}
.red          { color: red}
div p         { color: red}
div p.red     { color: red}
#first_id     { color: red}
```
以及直接使用inline的方式:
```html
  <p class='red' style='color: red'>第一个div</p>
```

但是, 不同的selector, 它们的权重(weight)是不同的.

Selector | 权重( weight)
---|---
!imporant | 无限大
inline | 1000
id     | 100
class  | 10
tag    | 1

我们看下面的代码:

```html
<style>
p             { color: red}               /* 权重 1 */
div p         { color: blue}              /* 权重 2 */
.red          { color: yellow}            /* 权重 10 */
div p.red     { color: green}             /* 权重 12 */
#first_id     { color: chocolate}         /* 权重1000 */
p             { color: silver !important} /* 权重无限大 */
</style>

<div class='parent'>
  <div id='first_id' class='first_class'>
    <p class='red' style='color: orange'>我是个div</p>
  </div>
</div>
```

下面结果来自 chrome developer tool: inspector

![CSS选择器权重](http://image.happysoft.cc/image/13/css_selector_weight.jpg)


## 常见的样式
TODO
