###View中的标签
`<Alloy>`是view的根标签，是每个controller对应UI的入口标签。在Alloy标签内有许多重要的二级标签，如Window、Require等。
XML中的每个标签元素，都是对应的Ti.UI为命名空间的对象子集。例如,<Label>是Ti.UI.Label的实例。每个对应的标签都能在Ti.UI的中找到，当然有些特殊用途的标签除外。

下面罗列一些重要的标签：

| 标签  | 用途                                        |
|:-----:|:------------------------------------------  |
| Alloy  |view的根标签                                |
| Require|引用widget或者引用其他的view                |
| Model  |引用modle或者                               |
| Module |引用一个Module中的页面                      |
| Widget |引用widget                                  |
| Collection|引用一个特定的collection                 |

index.xml作为APP的UI入口文件，其<Alloy>中只能放特定的子标签。下面标签是被允许的：
* Ti.UI.Window `<Window>`
* Ti.UI.TabGroup `<TabGroup>`
* Ti.UI.iOS.NavigationWindow `<NavigationWindow>`
* Ti.UI.iPad.SplitWindow `<SplitWindow>`


####Require 标签

<Require>主要有两个作用：导入外部的view和导入widget。

#####导入外部的view
使用Require标签，使用src属性字段指明导入的view的名字，不需要加'.xml'后缀名。标签内可以使用type属性表明导入view的类型，Titanium默认该属性值为"view"。通常会在标签内声明该标签的id以便在controller中调用。
```xml
app/views/label_page.xml

<Alloy>
    <Window>
        <Label id='label_out' backgroundColor="blue" borderRadius='5' text="this is a label"/>
    </Window>
</Alloy>
```

```xml
app/views/image_view.xml

<Alloy>
    <Window>
        <ImageView id='image_out' image="http://www.baidu.com/img/bdlogo.png">
    </Window>
</Alloy>
```


```xml
app/views/index.xml

<Alloy>
    <TabGroup>
        <Tab>
            <Require type='view' src='label_page' id='label'>
        </Tab>
        <Tab>
            <Require type='view' src='image_view' id='image'>
        </Tab>
    </TabGroup>
</Alloy>
```
如上在index.xml中引用了label_page和image_view两个view，并分别分配了id。在controller中可以通过$.requireId.getView('objectId')来访问被引用view中的对象元素。
例如：

```javascript
app/controllers/index.js

var label_imported = $.label.getView('label_out');
console.info(label_imported.text); //>this is a label
var image_imported = $.image.getView('image_out');
image_imported.setImage('https://www.google.com//images/srpr/logo11w.png');
```

#####导入widget
view中导入widget可以使用`<Widget>`，或者使用`<Reruire>`并将type属性设置为‘widget’,两种方法是等价的。widget的导入需要先将widget放到对应文件目录中，然后使用`<Widget>`或者使用`<Rrequire>`进行导入，具体方法参见Widget的相关章节。


#####参数传递



#####添加子视图

当在view中使用`<Require>`标签时，可以给`<Require>`添加子标签，然后在被require的view所对应的controller中添加其子标签,在controller中使用`arguments[0]`来获取所添加的子标签。例如：

```xml
app/views/wrapper.xml

<Alloy>
    <View width='100%' borderWidth='1' borderRadius='3'/>
</Alloy>

```
```javascript
app/controllers/wrapper.js

var args = arguments[0] || {};
//使用underscore的方法来添加子元素
_.each(args.children || [],function(child){
    $.wrapper.add(child);
});

```
```xml
app/views/index.xml

<Alloy>
    <Window>
        <Require src='wrapper'>
            <Label text='Hello'/>
            <Button title='press me'/>
        </Require>
    </Window>
</Alloy>
```

####Model标签
使用`<Model>`导入一个model，在controller中可以通过`Alloy.Models.model_name`来调用被导入的model。如果给`<Model>`添加一个id，则可以通过`$.id`直接调用被导入的model。`<Model>`为`<Alloy>`的子标签。
```xml
<Alloy>
    <Model src='students'/>
    <Window>
        <View backgroundColor='#86D3F0' height='Ti.UI.SIZE'>
    </Window>
</Alloy>
```
```javascript
var student = Alloy.Models.students;
var name = student.get('name');
var sex = student.get('sex');
```

使用`<Model>`可以在当前的controller创建一个model的instance(实例)，并且需要给标签加上属性`instance='true'`。
```xml
<Alloy>
    <Model src='students' id='students_model' instance='true'/>
    <Window>
        <View backgroundColor='#86D3F0' height='Ti.UI.SIZE'>
    </Window>
</Alloy>
```
```javascript
var student = $.students_model;
var name = student.get('name');
var sex = student.get('sex');
```

####Module属性
使用`Module`属性可以在view中导入一个CommonJS的module。使用方法有以下两点:
* CommonJS的Module需要放在`app/lib`文件夹下。CommonJS的Module需要暴露一个`pulic`的方法,方法名为`createXXXX`,并且需要返回一个`UI Object`类型。其中`XXXX`会作为xml的标签名被添加到view中。
* 将<XXXX>标签添加到目标view的xml中，其module属性值为module的文件名(省略后缀名)。在标签中可以定义自定义的一些参数，作为module的输入参数。

```javascript
app/lib/block.js

//args为从xml标签中获取的参数
exports.createBlock = function (args){
    var imageArgs = {
    image: args.imageUrl,
    height: 200
    };
    var imageView = Ti.UI.createImageView(imageArgs);
    //返回一个ImageView添加到view中
    return imageView;
}

```
```xml
app/views/index.xml

<Alloy>
    <Window>
        <Block module='block' imageUrl='http://www.baidu.com/img/bdlogo.png'/>
    </Window>
</Alloy>
```

####Module标签
使用`<Module>`可以导入一个原生Module中的view。

后面补充。。。。。。。。。
