关于机型适配你必须知道的技巧

  众所周知，移动端的开发都会有一个很棘手的问题，这个问题就是不同机型的适配。作为开发人员，大量的时间可以专注在业务的处理
和产品的评估上，那么机型适配我们必然要有一个很好的解决方案。Titanium作为跨平台开发技术，机型的适配必然是一个痛点也是重点
以下就是我们公司在机型适配上采取的两种相对高效和可以解放大量生产力的方法。大部分Titanium使用了Alloy框架，Alloy框架的使用，
可以把复杂的逻辑转换成mvc这种简单的开发模式，但是同时也带来
一定的适配问题，所以我们的方法是将样式全部写在stss文件中，不要在试图层嵌入大量的样式代码。这样会在机型适配和样式调整上都会
带来大量的问题。将样式写在stss里面，我们用不同机型的Label适配为例:

第一种方案:

```
// Default label
"Label": {
    backgroundColor: "#000",
    text: 'BlackBerry or another platform'
},
 // iPhone
"Label[platform=ios formFactor=handheld]": {
     backgroundColor: "#f00",
     text: 'iPhone'
  },
// iPad and iPad mini
"Label[platform=ios formFactor=tablet]": {
     backgroundColor: "#0f0",
     text: 'iPad'
  },
// blackberry and mobileweb
"Label[platform=blackberry,mobileweb]":{
     text: 'blackberry and mobile web'
  },

// not ios
  "Label[platform=!ios]":{text: "I am not ios!"}
```
但注意以下几点:
1. "Label"与"[platform" 之间，不能有空格！
2. platform 可选的值，是android, ios, blackberry, mobileweb
3. formFactor 表示作用于  phone(=handheld) 还是pad (=tablet),
4. 多个平台，可以使用 platform=android,ios
5. 如果不希望作用于某个平台，使用！， 例如： platform=!ios

