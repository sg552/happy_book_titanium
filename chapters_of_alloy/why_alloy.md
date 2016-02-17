# Alloy 与 DSL

## Alloy 初体验

Alloy 的思想有点儿过于先进，目前还没有厂商给出太好的支持。

Alloy 如果是2.0的开发方式的话， 传统的Titanium开发就是1.0的方式。我们做个
对比：

Titanium 1.0:

```js
window = Ti.UI.createWindow({
    backgroundColor: 'blue';
});

label = Ti.UI.createLabel({
    color: 'red';
    text: 'Hello world!';
});

window.add(label);
window.open();
```

如果我用 Alloy的方式：

app/controllers/index.js

```javascript
$.index.open();
```

app/views/index.xml

```xml
<Alloy>
  <Window class="container" style="">
    <Label>Hello, World</Label>
  </Window>
</Alloy>
```

app/styles/index.tss

```css
.container: {
  backgroundColor:'green';
}

Label{
  color: 'red';
}
```

## DSL ：领域专用语言

DSL的功能极其强大。很多地方必须用DSL才能描述清楚，它就在咱们的身边，
例如：

### 数学公式
```
DSL: 1 + 1 = 2
非 DSL: 一加一等于二
```

好像没啥感觉。看看下图：

![复杂的公式](/images/fuza_gongshi.jpg)

如果用文字的话是没法描述的。


### 音乐乐谱

```
非 dsl: 都 来 咪 发 嗖 啦 西 都
简谱 : 1 2 3 4 5 6 7
```

这个如何用简谱表示呢？

![复杂的五线谱](/images/wuxianpu.png)


### 化学公式

可以用汉字表示一些简单的概念：

C: 碳
H: 氢
CO2:  二氧化碳

对于下图，该如何用汉语表示呢？

![复杂的分子式](/images/fenzishi.gif)


### 若干编程世界中的 DSL

可以看出，越是在某个领域中变得复杂，就越是需要一种特定的表达语言。

下面是我们常见的DSL，希望大家能用好它们：

- 样式 : 用 css, sass, tss
- 视图 : XML, jade/haml
- 配置文件 : .properties, .yaml
- 业务逻辑 : java/ruby/python...
- 数据库 : SQL, (non SQL)
- 自动化脚本 : rake, ant, maven, grunt
