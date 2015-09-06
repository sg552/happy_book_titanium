#Ti.UI.Label

**Label**是Titanium UI组件中最常用的一个**文本**显示UI组件，常被用来处理页面中**较短**或**中长型**的文本显示；非
必要情况下我们不建议使用Label来处理长文本和超长型的文本显示，非必要的情况下对于长文本我们建议你使
用**文本域**(Ti.UI.TextArea)UI组件(详见**2.4.x**)。下面是一个Label的例子，你在Hello World项目中就已经接触过了：

```
    <Alloy>
        <Window class="container" id="my_window">
            <Label id="label" onClick="doClick">Hello,World</Label>
        </Window>
    </Alloy>
```

我们也可以在**.js**文件中动态创建Label：

```
    var my_label = Ti.UI.createLabel({
        id:'label',
        width:'100%',
        height:'10%',
        text:'Hello,World'
    });

    my_label.addEventListener('click',doClick(e));   //label的点击事件，相当于.xml中的“onClick=doClick”
    $.my_window.add(my_label);                       //将创建的label添加到Window页面中
```

##1.Label常用的几个属性
