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

## 调试CSS的方法:

### 普通的方法
在编辑器中修改代码, 保存, 切换到浏览器窗口,刷新.

### 推荐的方法

使用 developer tools. 在所有浏览器中都是这个名字. 用法几乎一样.
用小放大镜图标,找到你希望修改的元素, 点击之, 会看到对应的所有属性.
点击任意一个属性, 输入数字,或者按键盘的 上下箭头, 即可用 "所见即所得"的方式来调试页面.
对于调整: 字体大小, div的 margin/padding/border的 top, left 值.特别有效.

## 常见的样式

名称        | 说明 | 例子
---         |---   | ---
color       | 字体颜色      | red, #ececec
font        | 字体全部属性  | italic bold 12px/30px arial,sans-serif;
background  | 背景          | #00FF00 url(bgimage.gif) no-repeat fixed top;
border      | 边框          | 1px solid red
margin      | 外边距        | 1px 3px 1px 3px
padding     | 内边距        | 5px 10px 5px 10px
float       | 浮动方式      | left, right
clear       | 清除前面的浮动| left, right, both
display     | 显示方式      | none, block, inline
width       | 宽            | 100px
height      | 高度          | 200px
position    | 布局          | absolute, relative
z-index     | 显示在上方的层次 | 0,1,100
list-style  | list 属性     | square inside url('/i/arrow.gif');

## 有用的pseudo class (伪类)

pseudo class 有7个,其中两个很常用,可以大大简化CSS:

伪类名称  | 说明
---       |---
:focus    | 表单项在输入状态的样式
:hover    | 某个元素被鼠标悬停时的样式

所以,我们这样声明:

```html
<style>
.my_div{ background-color: red }
.my_div:hover{ background-color: green }
</style>

<div class='my_div' style='width: 100px; height: 100px'></div>
```

就可以看到, 鼠标一移动到这个div上,这个区域就从 红色 变成了绿色

## Box-Modeling 盒子模型(margin, border, padding的关系)

如下图.  最外层的红色是外边距(margin), 最内层的绿色是内边距(padding), 中间的黑色粗线是border.

我们为某个div设置width/height时,指的都是border的宽和高.

![div盒子模型](http://image.happysoft.cc/image/14/box-modeling.jpg)

## 定位(Positions)

分成: static(默认), float, relative, absolute 等.

### static(默认布局)

一个div就占一行. 各种元素以出现在HTML中的顺序为准.

### float(浮动定位)


### relative(相对定位)

出现在与它 父类元素的 相对位置. 例如:

```html
<div style='width: 200px; height: 200px; border: 1px solid blue' >
  <div style='position:relative; left: 50px; top: 80px;
    width: 50px; height: 50px;
    background-color: red; '>
  </div>
</div>
```
看起来就是:
<div style='width: 200px; height: 200px; border: 1px solid blue' >
  <div style='position:relative; left: 50px; top: 80px;
    width: 50px; height: 50px;
    background-color: red; '>
  </div>
</div>

### absolute 绝对定位

它的参照父类元素是最上一个 "absolute, 或者 relative" 的元素,
而不是最近父类的元素.

出现的位置是标注的top,left位置上. 例如, 下面有三个 div,  最内侧的 div是absolute ,
第二个div是普通的static 定位, 所以, 第三个div就会以最外层的div做参照.

```html
<div style='width: 300px; height: 300px; border: 2px solid red; position: relative'>
  <div style='width: 200px; height: 200px; border: 1px solid blue; margin: 100px;' >
    <div style='position:relative; left: 50px; top: 80px;
      width: 50px; height: 50px;
      background-color: red; '>
    </div>
  </div>
</div>
```
看起来就是(注意: 第三个 div出现在了第二个div之外)

<div style='width: 300px; height: 300px; border: 2px solid red; position: relative'>
  <div style='width: 200px; height: 200px; border: 1px solid blue; margin: 100px;' >
    <div style='position:absolute; left: 50px; top: 80px;
      width: 50px; height: 50px;
      background-color: red; '>
    </div>
  </div>
</div>


## 数值属性的简写

对于 margin/padding 等描述"上,右,下,左"的数值属性,我们发现它可以这样写:

```css
margin-top: 5px;
margin-right: 10px;
margin-bottom: 5px;
margin-left: 10px;
```

等同于下面三种形式:

```css
margin: 5px 10px 5px 10px;
margin: 5px 10 5 10;
margin: 5px 10px;
```


