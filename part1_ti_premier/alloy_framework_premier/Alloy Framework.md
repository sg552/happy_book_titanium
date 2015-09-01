#1.Alloy 概述

Alloy是Titanium自带的一个Mobile App开发框架模型(template)，也是Titanium默认的一个开发框架模型。Alloy框架基于**[MVC(Model View Controller)](http://baike.baidu.com/link?url=VeL0t6kbMGxDJwLZtyUM0Z48SN29PR4-8WyYWso8jDfmsLcVBPufn1ldTGjxOmLTGKoa05FhIDB2tng4hiEMh6a6ISaoD_f5qGPcrtDHHizVQ4xFsrZJ4VFrYPCEzgmm)**开发模型，将App的“逻辑”、“数据”和“界面”三大模块分离开来各自编写、组织自己的代码，但同时三者又互相逻辑关联；这正是MVC开发框架最独特的特色和优势。MVC的
开发框架很好的处理并划分了不同逻辑功能块处理各自的逻辑业务，使得开发任务的分配和管理更加明确，是一种很好的团队协作开发模式；Alloy开发框架则很好的继承了MVC这种优势。

Alloy开发框架具有十分良好的“数据绑定”和“js”内嵌支持，这要归功于Alloy对**[Backbone.js](http://docs.appcelerator.com/backbone/0.9.2/)**和**[Underscore.js](http://underscorejs.org/)**的支持。这使得Alloy在业务逻辑编码上，使用js更加的得心应手。
Backbone.js为应用提供一套类同于“MVC”结构式的服务支持：

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

    Two-tabbed Alloy Application这个模板在默认模板基础上，为项目添加了两个“tab”，即在App的页面底部
    会有两个默认的窗口切换键。

    Titanium项目模板除了自带的Alloy MVC框架之外，Titanium允许开发者自定义适合自己的项目模板，这些模板在
    Classic中都可以找到。

#2.Alloy 开发框架

Alloy开发框架基于MVC框架设计，那么在项目的结构目录上则有很明显的树形“分类”，不同的文件夹管理不同
类型的文件。下面，我们将以Alloy默认的“Hello World”项目模板进行介绍：

    (这里插图：Hello World项目的文件树形结构)
从上面的图中我们可以看到项目有3个主要的文件夹和一些配置文件。其中，我们的大部分编码工作都将app
这个目录下进行。
##2.1 app文件夹
在该目录下我们看到有“assets、controllers、models、styles、views”5个主要的文件夹，和一些配置性的文
件。assets文件和大多软件项目中的“assets”文件夹的属性一致，该文件夹用来存放项目中所有要用到的“媒体
性文件(图片，音频，影频文件等等)”；不过Alloy将不同的系统平台区别开来，每个系统平台都有自己的一个专
属文件夹，在一定程度上对不同的系统平台对媒体文件的尺寸和格式不同的需求做好了管理。Models则文件夹里
面包含所有的数据处理.js文件，通常都用来处理App在本地数据库(Sqlite)的数据绑定、读取等处理。我们重点
介绍“controllers、styles、views”3个文件夹。

###2.1.1 views
views包含项目的所有的UI文件(这里指静态定义的UI控件)。一般情况下，一个.xml文件代表App中的一个页面
(里面包含了窗口window UI控件)。index.xml：

```
    <Alloy>
        <Window class="container">
            <Label id="label" onClick="doClick">Hello,World</Label>
        </Window>
    </Alloy>
```
在这个文件中，一共有3种“标签”：Alloy、Window和Label，以及他们的属性。Alloy标签
