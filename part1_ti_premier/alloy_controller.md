# Alloy Controllers


##什么是Controllers

* 在 `app/controller`目录下面
* 用 `javascript` `js` 文件
*  *View* 视图对 *UI* 的控制
* 与 `model` 进行沟通

##Controllers与Views的关联

参照如下例子(*3-1*)：

*app/controllers/index.js* :

```
function doClick(e){	
	alert($.myLabel.text);	
}	
$.index.open()
```

*app/views/index.xml* :

```
<Alloy>	
	<Window class=“myWin”>	
		<Label id=“myLabel” onClick=“doClick”>Hello</Label>
	</Window>	
</Alloy>	
```

通过*3-1*例子能整理出两者之间的关联:

`$.myLabel` : **controller**通过`$`+`id`这种特殊的方式`$.<id>`，能够获取到**view**视图定义好的实例对象，并且能够通过它拿到并设置它的属性。

例如`$.myLabel.text = "newText"` `$.myLabel.hide()`等等。

需要特别提及的是**View**中的**top-leve UI**(最顶级的容器)有默认的id,如*3-1*中的`window`有默认的`id`,通过*index.js*中的`$.index.open()`能够直接获取它的对象调用打开的方法。默认值为当前`controller`文件名。


##controller与其他controller和view的关联

可以通过下面的方式获取其他controller的对象，获取它的视图并打开。
```
Alloy.createController(“myController”).getView().open();
```

上面的整块代码可以拆分为三个步骤:

* `
controller ＝ Alloy.createController(“myController”)
`获取一个`controller`实例。

* `view = controller.getView()`拿到对应`controller`的视图窗口。

* `view.open()`调用`view`的打开事件，这样就能够与其他`controller`进行关联了。


## require controller

用**BackBone.Events**来发送事件，*index*能够`require`(调用)其他的*controller*并触发它的监听事件。

*app/views/index.xml* :

```
<Alloy>	
	<Window>	
		<Require id=“myLabel” src=“myLabelFile” onNotify=“dosth”/>
	</Window>	
</Alloy>	
```

*app/views/myLabelFile.xml* :

```
<Alloy>	
	<Label id=“myLabel” onClick=“pressClick”>Hello</Label>
</Alloy>	
```

*app/controllers/myLabelFile.js* :

```
function pressClick(e)	{	
	$.trigger(‘notify’);	
}	
```

当`index`里的`label`被`click`的时候,会触发*myLabelFile controller*里面的`pressClick()`事件。

## 继承，现在很少用，不写

## 特殊常量

* `OS_ANDROID`/`OS_IOS`/`OS_MOBILEWEB`/`OS_WINDOWS`(>= Alloy 1.6.0)
* `ENV_DEV`/`ENV_TEST`/`ENV_PRODUCTION`	(>= Alloy 1.4.0)
* `DIST_ADHOC`/`DIST_STORE` (>=Alloy 1.4.0)

## controller之间的传参

下面是需要往下一个页面之间传递参数时的例子:

*app/controllers/index.js*

```
var argSet = {
	title: “myHtle”,		
	url: “www.baidu.com”	
};	
var myView=Alloy.createController(“myTableView”,argSet).open();
```

*app/controllers/myTabelView.js*

```
var args = arguments[0] || {};	
var title = args.title || ‘’;	
var url = args.url || ‘’;	
```
在`controller`创建的时候在第二个参数加上自己想要传递的内容,在下一个页面用`var args = arguments[0] || {};`来接受传参。

## 全局的命名空间

能够在不同的controller引用全局的命名空间里面的对象或变量。

*app/controllers/index.js*
```
$.index.open();
Alloy.Globals.parent = $.index;
```

可以在别的`controller`文件里面对`index`进行操作:
*app/controllers/other.js*
```
var parent = Alloy.Globals.parent;
parent.close();
```

## 初始化文件

`app/alloy.js`在软件运行的生命周期中存在,并且是优先于`index.js`就在程序的初始化的时候执行。

`alloy.js`里面的方法能够被覆盖和全局的引用。`app/alloy.js`也能够访问`Alloy.Globals`命名空间。

## CommonJS（require其他的js文件）

*app/libs/help.js*

```
function say_hello(name){
    alert('hello'+name);
}
exports.say_hello = say_hello ;
```
*app/controller/index.js*

```
var help = require("help") ;
help.say_hello("xuan");
$.index.open();
```
*输出:*

```
> hello xuan
```

同样 commonjs能够支持不同机型,如下面的文件树状图:

```
app/
├──lib
│  ├──ios
│  │   └── help.js
│  └── help.js
├──models
├──styles
└──views
   └── index.xml
```