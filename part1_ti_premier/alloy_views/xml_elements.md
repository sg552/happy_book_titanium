###View中的标签
<Alloy>是view的根标签，是每个controller对应UI的入口标签。在Alloy标签内有许多重要的二级标签，如Window、Require等。
XML中的每个标签元素，都是对应的Ti.UI为命名空间的对象子集。例如,<Label>是Ti.UI.Label的实例。每个对应的标签都能在Ti.UI的中找到，当然有些特殊用途的标签除外。
下面罗列一些重要的标签：

| 标签  | 用途                                       |
|:-----:|:------------------------------------------ |
|Alloy  |view的根标签                                |
|Require|引用widget或者引用其他的view                |
|Model  |引用modle或者                               |
|Module |引用一个Module中的页面                      |
|Widget |引用widget                                  |
|Collection|引用一个特定的collection                 |

index.xml作为APP的UI入口文件，其<Alloy>中只能放特定的子标签。下面标签是被允许的：
* Ti.UI.Window <Window>
* Ti.UI.TabGroup <TabGroup>
* Ti.UI.iOS.NavigationWindow <NavigationWindow>
* Ti.UI.iPad.SplitWindow <SplitWindow>


####Require 标签

<Require>主要有两个作用：导入外部的view和导入widget。

#####导入外部的view
使用Require标签，使用src属性字段指明导入的view的名字，不需要加'.xml'后缀名。标签内可以使用type属性表明导入view的类型，Titanium默认该属性值为"view"。通常会在标签内声明该标签的id以便在controller中调用。```xml
app/views/label.xml

<Alloy>
    <Window>
        <Label backgroundColor="blue" borderRadius='5' text="this is a label"/>
    </Window>
</Alloy>


app/views/image_view.xml

<Alloy>
    <Window>
        <ImageView image="http://www.baidu.com/img/bdlogo.png">
    </Window>
</Alloy>


app/views/index.xml

<Alloy>
    <Window>
    </Window>
</Alloy>
```
