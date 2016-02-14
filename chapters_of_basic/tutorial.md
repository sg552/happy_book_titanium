# 实战：Titanium中国开发者论坛App

我们要做一款真实的App. 不如就为Titanium中国开发者论坛做个App吧！躺在床上
还可以刷一刷屏，灌灌水~

特性如下：

- 有启动图，有个像样的图标
- 可以看到titanium 中国社区的分论坛(Forum)
- 点击任意分论坛后，可以看到该分类下所有话题(Topic)
- 点击任一标题，可以看到该话题下所有的帖子(Post)

## 需要的接口已经备好

- 看到所有的论坛

http://tidev.in/interface/forums

```
[
  {
    id: 1,
    name: "开发知识",
    description: " 大家关于开发的讨论"
  },
  {
    id: 2,
    name: "作品展示",
    description: "有哪些成功的Titanium作品，大家都发上来吧！ "
  },
  {
    id: 3,
    name: "其他话题",
    description: " 介绍，认识，线下活动，工作机会等。征基友也行。"
  }
]
```

- 看到某个论坛下所有的文章

需要的参数： forum_id （分论坛id)

http://tidev.in/interface/topics?forum_id=3

```
{
  forum_id: 3,
  forum_name: "其他话题",
  topics: [
    {
      title: "［北京］诚聘　titanium / ruby 全栈攻城狮 人数不限",
      topic_id: 13,
      user: "思维"
    },
    {
      title: "北京招聘titanium开发者",
      topic_id: 43,
      user: "思维"
    }
  ]
}
```

- 看到某个论坛下的所有文章

http://tidev.in/interface/posts?topic_id=64

需要的参数： topic_id (标题id)

```
{
  title: "明星框架 已经开源了",
  topic_id: 64,
  posts: [
  {
    html_body: "<p>欢迎大家多发 pull request:</p>
  <p>https://github.com/star-framework/star-framework</p>",
    user: "思维",
    created_at: "2016-02-10 07:30:38"
  }
  ]
}
```


## 新建titanium项目

过程如同前一章。略

## 实现基本功能：论坛列表

进入到app时，应该向远程发起请求，获得数据后，打开第一个视图，就应该是列表视图。

```js
// 文件： Resources/app.js:
// 向远程发起请求，
var http = Ti.Network.createHTTPClient({

  // 成功后，打开 论坛列表页 (forums.js)
  onload: function(e){
    var response = JSON.parse(this.responseText);
    // 这里使用了 require 来加载代码。 forums.js 位于 app.js 同级目录
    require('forums')().open();
  },
  onerror: function(e){
    alert('网络不好:' + e);
  }
});

http.open('GET', 'http://tidev.in/interface/forums');
http.send();
```

由于使用了`module.exports`, 接下来的这句代码:

```js
require('forums')().open();
```

等同于下面三句：

```js
ForumsWindow = require('forums');
temp = new ForumsWindow();
temp.open();
```

论坛列表页如下：

```js
// 文件： Resources/forums.js
// 本方法通过下面方式来调用： require('forums')().open();
ForumsWindow = function(){

  // 创建window
  var window = Ti.UI.createWindow({ })

  // 在创建ListView 之前，需要先创建一个template, 用于设置样式
  var my_template = {
    childTemplates:[
      {
        type: 'Ti.UI.Label',
        bindId: 'forum_name',
        properties:{
          width: 300,
          height: 20,
          left: 0
        }
      },
      {
        type: 'Ti.UI.Label',
        bindId: 'forum_description',
        properties: {
          width: 300,
          height: 40,
          top: 20,
          left: 0
        }
      }
    ]
  }

  // 创建 ListView
  var list_view = Ti.UI.createListView({
    templates: { 'template': my_template },
    defaultItemTemplate: 'template'
  });

  // 创建ListSection
  var sections = [];
  var section = Ti.UI.createListSection();

  // 加上临时的假数据
  var data = [
    {
      forum_name: { text: '论坛1'} ,
      forum_description: { text: '1号论坛的描述' }
    },
    {
      forum_name: { text: '论坛2'} ,
      forum_description: { text: '2号论坛的描述' }
    }
  ]
  section.setItems(data);
  sections.push(section);
  list_view.setSections(sections);
  window.add(list_view);

  // 返回window对象
  return window;
}

module.exports = ForumsWindow;
```

现在，我们运行：

```
$ ti build --platform=ios
```

可以看到，列表出来了(数据是假的，样子很难看)：

![列表，假数据](/images/basic_tutorial_jia_shu_ju.png)

## 实现基本功能：某个论坛下的话题(topic)列表

点击任意一个论坛，显示所有的话题列表

## 实现基本功能：查看帖子

点击任意一个话题，可以查看该话题的所有帖子。

## 修改app的图标


## 修改app的名字

修改 tiapp.xml :

```
	<name>Ti中文社区</name>
```

