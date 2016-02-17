# 概述

**Alloy**是**Titanium**自带的一个Mobile App开发框架模型(template)，也是Titanium默认的一个开发框架模型。Alloy框架基于**[MVC(Model View Controller)](http://baike.baidu.com/link?url=VeL0t6kbMGxDJwLZtyUM0Z48SN29PR4-8WyYWso8jDfmsLcVBPufn1ldTGjxOmLTGKoa05FhIDB2tng4hiEMh6a6ISaoD_f5qGPcrtDHHizVQ4xFsrZJ4VFrYPCEzgmm)**开发模型，将App的“逻辑”、“数据”和“界面”三大模块分离开来各自编写、组织自己的代码，但同时三者又互相逻辑关联；这正是MVC开发框架最独特的特色和优势。MVC的
开发框架很好的处理并划分了不同逻辑功能块处理各自的逻辑业务，使得开发任务的分配和管理更加明确，是一种很好的团队协作开发模式；Alloy开发框架则很好的继承了MVC这种优势。

Alloy开发框架具有十分良好的“数据绑定”和“js”内嵌支持，这要归功于Alloy对**[Backbone.js](http://docs.appcelerator.com/backbone/0.9.2/)**和**[Underscore.js](http://underscorejs.org/)**的支持。这使得Alloy在业务逻辑编码上，使用js更加的得心应手。
Backbone.js为应用提供一套类同于“**MVC**”结构式的服务支持：

     M：类同于Model，提供key-value形式的数据绑定和自定义事件的服务支持。
     V：类同于View，通过使用JSON格式的接口调用API来处理被设置监听事件的控件的逻辑业务。
     C：类同于Controller，这里为Collections，是所有函数API的集合群。

Underscore.js，Underscore是JavaScript一个库(library)，这意味着你能直接使用JS绝大多数的内置函数和功能支持，而不需要再去继承“基类”。

在Alloy开发框架中：

    M：代表Model，处理应用(application)所有的数据绑定等数据业务，主要使用到Backbone的Model和Collection，使用js进行编码。

    V：代表View，应用的UI层。Alloy使用XML(Extensible Markup Language，对应.xml文件)搭建UI控件，使
       用Titanium Stylessheets(对应.tss文件)定义控件的样式(类同html中的.css)。

    C：代表Controller，M/V的衔接层，处理所有监听事件和逻辑业务。调用Alloy API和Titanium API。

在Titanium中新建一个项目时，在项目模板“Project Template”选择时，Titanium会默认选择一个Default
Alloy Project，这个项目就是典型的“Hello World”例子；默认模板会搭建好所有的文件管理骨架，开发者只要
在不同的文件夹中进行代码编写就可。不过，Titanium还提供其他的项目模板：

    **Two-tabbed Alloy Application**这个模板在默认模板基础上，为项目添加了两个“tab”，即在App的页面底部
    会有两个默认的窗口切换键。

    Titanium项目模板除了自带的Alloy MVC框架之外，Titanium允许开发者自定义适合自己的项目模板，这些模板在
    **Classic**中都可以找到。

#2.Alloy 开发框架
Alloy开发框架基于MVC框架设计，那么在项目的结构目录上则有很明显的树形“分类”，不同的文件夹管理不同
类型的文件。下面，我们将以Alloy默认的“Hello World”项目模板进行介绍：

    (这里插图：Hello World项目的文件树形结构)
从上面的图中我们可以看到项目有3个主要的文件夹和一些配置文件。其中，我们的大部分编码工作都将在**app**
这个目录下进行。

##2.1 app文件夹
在该目录下我们看到有“**assets**、**controllers**、**models**、**styles**、**views**”5个主要的文件夹，和一些配置性的文
件。assets文件和大多软件项目中的“assets”文件夹的属性一致，该文件夹用来存放项目中所有要用到的“媒体
文件(图片，音频，影频文件等等)”；不过Alloy将不同的系统平台区别开来，每个系统平台都有自己的一个专
属文件夹，在一定程度上解决了不同的系统平台对媒体文件的尺寸和格式不同的需求问题。Models文件夹里
面包含所有的数据处理**.js**文件，通常都用来处理App在本地数据库(**Sqlite**)的数据绑定、读取等处理。我们重点
介绍“controllers、styles、views”3个文件夹。

###2.1.1 views
**views**包含项目的所有的UI文件(这里指静态定义的UI控件)。一般情况下，一个.xml文件代表App中的一个页面
(里面包含了窗口window UI控件)。*index.xml*：

```
    <Alloy>
        <Window class="container">
            <Label id="label" onClick="doClick">Hello,World</Label>
        </Window>
    </Alloy>
```

首先我们要注意这里的格式
在这个文件中，一共有3种“标签”：**Alloy**、**Window**和**Label**，以及他们的属性。Alloy标签是.xml中级别最高的父级
标签。Window是窗口标签，一对window标签对应一个窗口，用来创建窗口的。Label是普通的文字标签，用来显示文
字；上面代码里Label中间的“Hello,World”就是要显示的文字(string)，另外一种写法是：

```
    <Label id="label" text='Hello,World' onClick="doClick"></Label>
```

对于这种写法的标签中出现的“text”就是Label标签的一种“属性”。每种标签都有或多或少的属性，用于描述标
签的各种性质，如：长(width)、高(height)、在窗口中显示的位置(左边距left、上边距top)等等。除了这些标
签外，代码中出现的“class、id”字段则是该UI控件的样式属性，他们对应于**index.tss**文件；而“onClick”字段
则是声明该UI控件的“监听事件”属性，即“点击事件”属性，我们知道这些事件需要在controllers文件中进行处理，
对应于**index.js**文件。

###2.1.2 styles
**styles**包含项目所有UI控件的样式代码文件。一个**.tss**文件对应和它同名的**.xml**文件中所有UI控件的样式，*index.tss*：

```
    ".container":{
        backgroundColor:"white"
    }

    "#label":{
        font:{
            fontSize:12
        }
    }
```

在views中我们已经说过“**class(container)**、**id(label)**”是UI控件的样式属性，从上面的代码中我们可以看出所有的属性都必须
包含在“**""**”内，而其的设定值value则都包含在“**{}**”中(这些写法都是可以省去的，但要使用**jade**<简化xml>、**stss**<简化tss>等gem)。
如果value中的某个值含有多种声明(id label的font属性)，那么需要再次用“**{}**”包含起来。

我们可以看到，样式属性class与id在tss中的表示是不同的，class需要使用**“.”**，id则使用**“#”**；除此之外，class的优先级要大于id，
意思就是说如果对于某个value既写在class中又写在id中，那么这个value只会以class中的为标准而生效，如：

```
    //xml文件：
    <Label class="label_calss" id="label_id" onClick="doClick"></Label>

    //tss文件：
    ".label_class":{
        text:"Hello,Titanium"
    }

    "#label_id":{
        text:"Hello,World"
    }

    //在App页面中，你将看到的是“Hello,Titanium”而不是“Hello,World”。
```

虽然UI控件的样式代码是可以直接写在xml文件中的，但是这种做法失去了styles文件夹的作用和意义；styles文件的目的就是为了方便
管理和维护的UI控件的样式，那么我们就应该充分运用它。另外，当UI控件需要进行不同系统平台的适配时styles文件则很好的解决了这
个问题了。

除此之外，需要注意的一点是：一个UI控件只能有一个id属性(即id是唯一的)，并且适用一个class；但是一个class
属性可以适用于多个UI控件(即class共同的样式声明，class是公共的)。

###2.1.3 controllers
**controllers**包含项目所有的监听事件和业务逻辑处理代码。同样对应于其同名的*index.xml*文件，除此之外在xml文件中声明的函数
名必须与该文件中的函数名一致。*index.js*：

```
    function doClick(e){
        alert($.label.text);
    }

    $.index.open();
```

在该文件中，函数对**doClick**监听事件做了一个“alert逻辑处理”(以另一个弹出的小窗口的形式再次显示label的文字)；即当App页面中的
该**Label**监听到点击事件时就会触发这个“alert逻辑处理”。

从上面的代码中，我们可以看出可以通过**“$.”**的形式获取xml中UI控件的id，也就是说我们可以通过这种方式来控制UI的表现属性。
这也就是我们为什么在views中要强调一个UI控件只能有且只有一个专属id的原因；如果两个UI控件有相同的id，那么**.js**文件中的逻辑
中的逻辑处理将无法识别到底是哪个UI控件触发了监听事件，从而报错。

PS：需要注意的是**$.index.open**则不属于这种情况，因为**Titanium**默认是可以允许通过以**“$.+文件名”**的形式直接控制某个页面的；但是前
提是，该页面必须含有一个窗口。这种写法等同于下面的效果：

```
    <Window class="container" id="index">
    ....
```

###2.2 alloy.js
**app**文件夹下这个文件比较重要，该文件中用来编写App项目所需要的绝大多数的项目配置和依赖，以及整个App项目需要用到的全局变量或者函数
都可以在这里声明。

    这里应该添加一个全局变量或函数的例子

##2.2 platform
**platform**这个文件夹通常情况下的作用是对Android不同机型的图片尺寸适配，对于不同尺寸的Android机型该文件夹做了6中不同尺寸比例的区分并
分别创建了不同的文件夹目录。

##2.3 plugins
**plugins**这个文件夹用来管理项目所有要用到的插件(plugin)配置。

##2.4 tiapp.xml
**tiapp.xml**这是项目根目录下一个重要的配置文件，这些配置范围比较广，从项目的基本信息到项目的发布信息以及项目在不同手机平台上的相关、
设置都罗列在内。下面，我们通过文件来比较详细的介绍每块的设置*tiapp.xml*：

① 这一块配置信息主要包括了项目的创建时的一些基本信息，这些信息中大部分是可以更改的，有些信息更改时需要重新配置，不能直接在该文件中修改。

```
    <id>com.happysoft.GeekIpad</id>         //Appid(App发布时需要申请获得唯一的App ID，此时这里要保证必须与获取的App ID一致)
    <name>Geek-ipad</name>                  //App名称
    <version>1.0</version>                  //App的版本号
    <publisher>pro</publisher>              //App的发布者
    <url>http://www.happysoft.cc</url>      //App的url
    <description>undefined</description>    //App的描述(App申请发布时，填写描述会更新这里)
    <copyright>2015 by pro</copyright>
    <icon>appicon.png</icon>                //App的图标
```

② App在IOS平台上的一些相关配置，包括是否隐藏状态栏、是否允许横屏等等一系列设置。

```
    <ios>
        <plist>
            <dict>
                <key>UISupportedInterfaceOrientations~iphone</key>
                <array>
                    <string>UIInterfaceOrientationPortrait</string>
                </array>
                <key>UISupportedInterfaceOrientations~ipad</key>
                <array>
                    <string>UIInterfaceOrientationPortrait</string>
                    <string>UIInterfaceOrientationPortraitUpsideDown</string>
                    <string>UIInterfaceOrientationLandscapeLeft</string>
                    <string>UIInterfaceOrientationLandscapeRight</string>
                </array>

                <key>UIStatusBarHidden</key>
                <true/>

                ....

                <key>UIStatusBarStyle</key>
                <string>UIStatusBarStyleDefault</string>
            </dict>
        </plist>
    </ios>
```

③ App在Android以及其他平台上的一些相关设置，如：主题设置，添加SDK的读写权限，App在接听电话时的后台进程暂住等等设置。

```
    <android xmlns:android="http://schemas.android.com/apk/res/android"/>

    <mobileweb>
        <precache/>
        <splash>
            <enabled>true</enabled>
            <inline-css-images>true</inline-css-images>
        </splash>
        <theme>default</theme>
    </mobileweb>
```

④ App引用第三方**SDK**时的**module**设置。配置时，需要添加**SDK**所适用的系统平台以及该**module**的名称(详情请参看本书的 **第X章**)

```
    <modules/>

    //例子
    <modules>
      <module platform="iphone">add module name here</module>
    </modules>
```

⑤ App发布时所适用的手机系统平台设置。

```
    <deployment-targets>
        <target device="android">false</target>
        <target device="blackberry">false</target>
        <target device="ipad">true</target>
        <target device="iphone">true</target>
        <target device="mobileweb">true</target>
    </deployment-targets>
```

⑥ App所引用的**Titanium SDK**版本设置，以及**plugins**版本号设置；必须与引用的版本序列号保持一致。

```
    <sdk-version>3.5.1.GA</sdk-version>         //Titanium SDK版本设置

    <plugins>
        <plugin version="1.0">ti.alloy</plugin>
    </plugins>
```

整个App项目目录中除了上述介绍的几个比较重要的文件目录外，在项目编译运行后还会生成一个*Resources*文件夹。这个文件
夹是编译产生的，可以删掉。另外需要注意的一点时，Titanium在创建一个项目时默认有**index.js**、**index.tss**、**index.xml**三个文件，
这三个文件可以更改其内容但是不能更改名称，因为Titanium默认必须有个入口页面**index**。至此，我们已经介绍完了Alloy开发框架；实际
上只要记住Alloy框架基于MVC框架模式，我们只要在相关的文件目录下进行编码就可以(**controllers**文件目录下编写**.js**文件，处理项目的业务逻辑；
**views**文件目录下编写**.xml**文件，构建页面的UI；**styles**文件目录下编写**.tss**文件，适配UI的样式)。
