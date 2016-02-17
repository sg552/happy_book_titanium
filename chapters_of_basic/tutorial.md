# 实战：Titanium中国开发者论坛App

我们要做一款真实的App. 不如就为Titanium中国开发者论坛做个App吧！躺在床上
还可以刷一刷屏，灌灌水~

特性如下：

- 有启动图，有个像样的图标
- 可以看到titanium 中国社区的版面(Forum)
- 点击任意版面后，可以看到该分类下所有话题(Topic)
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

需要的参数： forum_id （版面id)

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

返回例子：

```
{
  title: "明星框架 已经开源了",
  topic_id: 64,
  posts: [
  {
    body: "欢迎大家多发 pull request:
  https://github.com/star-framework/star-framework",
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

### 先弄个大框出来

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

### 把假数据变成真数据

重新实现 app.js 中的 onload 方法，

```js
onload: function(e){
  var response = JSON.parse(this.responseText);

  // 设置好data的格式, 为了给ListView 使用
  var data = []
  for(i = 0; i < response.length; i++){
    data.push({
      forum_name: { text: response[i].name},
      forum_description: { text: response[i].description },
      // 这个forum_id 不需要放到ListView中，
      // 所以不需要再设置一个 { text: ... }
      forum_id: response[i].id
    });
  }
  // 把data 作为参数，传递到 forum.js 中去。
  require('forums')(data).open();
}
```

同时，修改 forums.js 文件：

```js
// 注意，这里增加了参数 data
Window = function(data){

  ...
  var section = Ti.UI.createListSection();
  // 这里直接使用data
  section.setItems(data);
  sections.push(section);
  ...
```

重新编译，运行，可以看到，真数据已经出现了：

![真数据](/images/basic_tutorial_zhen_shu_ju.png)

### 实现ListView中某一行的点击跳转

例如，我们要查看第一个版面的话题列表，就要点击第一行。所以，为它增加事件：

```js
//...
list_view.addEventListener('itemclick', function(e){
  forum_id = data[e.itemIndex].forum_id
  console.info('=== item clicked!' + JSON.stringify(e));
  // 下一步，根据这个 forum_id 来打开某个具体的版面
});

return win;
```
可以看出：

- 可以通过 e.itemIndex 来获取到点击ListView到具体的哪一行。
- 通过 data[e.itemIndex] 来获取data 数据中的内容
- 事件 e 有很多属性, 例如：
  - itemIndex: 点击在了哪个item上。这个是最常用的。
  - sectionIndex: 点击在了哪个section.
  - bindId: 点击在了哪个区域。是"forum_name" 还是"forum_description"

至此，我们对于“版面列表”的操作就完成了。

## 实现基本功能：某个版面下的话题(topic)列表

接下来，我们继续实现: 点击任意一个论坛，显示所有的话题列表。

修改 forums.js文件，继续完善其中的"itemclick"事件：
```js
list_view.addEventListener('itemclick', function(e){

  // 获取到点击的论坛id
  forum_id = data[e.itemIndex].forum_id

  // 拼成远程接口
  url = 'http://tidev.in/interface/topics?forum_id=' + forum_id;

  // 准备发起http请求
  var http = Ti.Network.createHTTPClient({
    onload: function(e){
      var response = JSON.parse(this.responseText);

      // 设置好data的格式。注意，这里开始，数据结构不同了。
      // forum_name: 版面的标题
      var data = {
        forum_name: response.forum_name
      }

      // topics: 所有话题。
      topics = []
      for(i = 0; i < response.topics.length; i++){
        temp = response.topics[i];
        topics.push({
          title: { text: temp.title},
          user: { text: temp.user},
          // 这个topic_id不需要放到ListView中，
          // 所以不需要再设置一个 { text: ... }
          topic_id: temp.topic_id,
        });
      }

      data.topics = topics;
      // 把data 作为参数，传递到 topics.js 中去。
      require('topics')(data).open();
    },
    onerror: function(e){
      alert('网络不好' + e);
    }
  });

  http.open('GET', url);
  http.send();
});

```

对于topic.js，代码如下；

```js
// topic.js 位于 Resources 目录下，与app.js 同级：
Window = function(data){
  var win = Ti.UI.createWindow({ })

  var my_template = {
    childTemplates:[
      {
        type: 'Ti.UI.Label',
        bindId: 'title', // 注意该bindId
        properties:{
          width: 300,
          height: 20,
          left: 0
        }
      },
      {
        type: 'Ti.UI.Label',
        bindId: 'user', // 注意该bindId
        properties: {
          width: 300,
          height: 40,
          top: 20,
          left: 0
        }
      },
    ]
  }

  var list_view = Ti.UI.createListView({
    templates: { 'template': my_template },
    defaultItemTemplate: 'template'
  });

  var sections = [];

  var section = Ti.UI.createListSection({
    // 设置好该section的标题
    headerTitle: data.forum_name
  });
  console.info(JSON.stringify(data.topics));
  section.setItems(data.topics);
  sections.push(section);
  list_view.setSections(sections);
  win.add(list_view);

  return win;
}

module.exports = Window;
```

可以看出，`topics.js`代码与之前的`forums.js`是一样的。只是在ListView的数据
展现方面略有差别（注意其中的template和data等变量结构）

![真实效果](/images/basic_tutorial_topics.png)

### 实现点击效果

接口是：

http://tidev.in/interface/posts?topic_id=64

需要的参数： topic_id (标题id)

返回例子：

```
{
  title: "明星框架 已经开源了",
  topic_id: 64,
  posts: [
  {
    body: "欢迎大家多发 pull request:
  https://github.com/star-framework/star-framework",
    user: "思维",
    created_at: "2016-02-10 07:30:38"
  }
  ]
}
```

现在，我们要点击任一话题，进入到该话题的详情页。为topics中的ListView增加事件：

```js
  list_view.addEventListener('itemclick', function(e){
    topic_id = data[e.itemIndex].topic_id;
    url = 'http://tidev.in/interface/posts?topic_id =' + topic_id;
    var http = Ti.Network.createHTTPClient({
      onload: function(e){
        var response = JSON.parse(this.responseText);

        // 设置好data的格式。
        var data = {
          topic_title : response.title
        }
        posts = []
        for(i = 0; i < response.posts.length; i++){
          temp = response.posts[i];
          posts.push({
            body: { text: temp.body},
            user: { text: temp.user},
            created_at: { text: temp.created_at }
          });
        }
        // 把data 作为参数，传递到 topics.js 中去。
        require('posts')(data).open();
      },
      onerror: function(e){
        alert('网络不好' + e);
      }
    });
    http.open('GET', url);
    http.send();
  });
```

接下来，我们要写最后一个页面： `posts.js`，它跟app.js也在同一目录下。

## 实现基本功能：查看帖子

点击任意一个话题，可以查看该话题的所有帖子。

接口：http://tidev.in/interface/posts?topic_id=31

```
{
  title: "run后遇到错误提示：当前超时设置为120000毫秒",
  topic_id: 31,
  posts: [
    {
      body: "刚new的一个project，只是想测试一下可不可以运行 ...",
      user: "一叶怀沙",
      created_at: "2015-09-21 16:57:34"
    },
    {
      body: " 不要使用安卓虚拟机（android SDK自带的 avd) ...",
      user: "思维",
      created_at: "2015-09-23 06:48:59"
    }
  ]
}
```

posts.js:

```js
Window = function(data){
  var win = Ti.UI.createWindow({
    backgroundColor: 'white'
  });

  // 使用 TableView 来解决问题，没有使用ListView
  var table_data = []
  for(var i = 0; i< data.posts.length; i++){
    temp_post = data.posts[i];
    var row = Ti.UI.createTableViewRow({
      height: Ti.UI.SIZE
    });

    // 帖子的正文
    var body = Ti.UI.createLabel({
      left: 0,
      top: 40,
      text: temp_post.body,
      height: Ti.UI.SIZE,
      borderColor: 'red',
      borderWidth: 3
    });

    // 发帖子的用户
    var user = Ti.UI.createLabel({
      text: temp_post.user,
      height: 20,
      left: 0,
      top: 20
    });
    // 发帖的时间
    var created_at = Ti.UI.createLabel({
      text: temp_post.created_at,
      height: 20,
      left: 100,
      top: 20
    });
    row.add(body);
    row.add(user);
    row.add(created_at);

    table_data.push(row);
  }

  var table_view = Ti.UI.createTableView({
    backgroundColor: 'white',
    data: table_data
  });

  win.add(table_view);
  return win;
}

module.exports = Window;
```

可以看到，最终的页面出来了：

![posts的页面](/images/basic_tutorial_posts.png)

## 增加导航栏

对于导航栏，我们可以在两个不同的平台上使用：

- iOS上，使用navigation window
- Android上，使用action bar.

为了演示，我们使用自定义的View来达到这一点。这个自定义的View位于页面的顶部，
有一个向左的箭头，表示返回。中间有标题。

/Resources/public.js 文件：
```
/*
 * Ti.App.navigation_window({
 *  title: '窗口的名字',
 *  back_function: function(){
 *    win.close();
 *    require('topics')().open();
 *  }
 * })
 *
 */
Ti.App.navigation_window = function(options){
  var title = Ti.UI.createLabel({
    text: options.title,
    center: 0,
    font: {
      fontSize: 25
    },
    color: 'black'
  })
  var back = Ti.UI.createButton({
    title: "返回",
    color: 'blue',
    font: 20,
    left: 0
  })
  var view = Ti.UI.createView({
    backgroundColor: 'white',
    height: 40,
    top: 20,
    left: 0
  })

  view.add(title);
  if(options.back_function){
    back.addEventListener('click', options.back_function)
    view.add(back);
  }
  return view;
}

```

然后，我们分别在三个页面加上对该函数的调用：

在 forums.js 中：
```js
require('public');
var navigation = Ti.App.navigation_window({
  title: '版面列表'
});
win.add(navigation);
```

在 topics.js 中：

```js
require('public');
var navigation = Ti.App.navigation_window({
  title: '话题列表',
  back_function = function(){
    win.close();
  }
});
win.add(navigation);
```

同时，让页面中的相应部分往下定位一定的距离：

```js
var list_view = Ti.UI.createListView({
  // ...
  top: 60
});
```

由于在最上方的navigation_window 中已经存在了`win.close()`, 所以，我们在原来
的js中的win.close()方法就不用调用了，把他删掉。

```js
  require('posts')(data).open();
  // 删掉这句
  // win.close();
```

## 美化UI页面

设置好每一行 ListView的宽度
```
var my_template = {
  childTemplates:[
     // ...
  ],
  properties: {
    height: Ti.UI.SIZE
  }
}
```

为posts页面加上背景色, 每一行的行高自适应：

```js
var body = Ti.UI.createLabel({
  left: 0,
  top: 40,
  text: temp_post.body,
  height: Ti.UI.SIZE,  // 行高
  backgroundColor: '#fafafa'  // 背景色
});
```

## 修改app的图标

app的图标，有180x180, 150x150，也有更高的1024x1024. 我们随便做个图标:

![ti china logo](/images/basic_tutorial_logo.png)

对于ios 来说, 要修改 DefaultIcon.png 这个文件.

这个文件名不需要在 tiapp.xml 中定义, ios会默认找到他.

对于android来说, 需要定义在 tiapp.xml 中, 使用 icon 这个节点, 名字必须是小写 a-z0-9

然后，修改`tiapp.xml`这个文件即可.

```xml
<!-- 这里定义了使用哪个文件作为图标 -->
<icon>appicon.png</icon>
```

我们把原来的两个文件替换掉：

- DefaultIcon.png  (针对于iOS)
- /Resources/android/appicon.png  （针对于Android)

文件删掉，把新的Logo换上去即可。

注意：这里最好使用原来的文件(根目录下的DefaultIcon.png 和 /Resources/android/appicon.png ) 作为命名。
否则的话，如果要改成 `my_icon.png` 注意的名字，我们还需要手动增加以下名字：

- my_icon-Small.png
- my_icon-Small@2x.png
- my_icon-Small@3x.png
- my_icon-Small-40.png
...

完整的屏幕看起来如下：

![screen with logo](/images/basic_tutorial_screen_with_logo.png)

## 修改app的名字

注意: 这里不能修改 `tiapp.xml` 中的<name> , 这个值很特殊, 它必须是英文,不能有空格. 例如:

```xml
<name>TiDevApp</name>
```

要想改名字的话,要使用 i18n 特性:

建立下面的文件结构(i18n与Resources处于同级目录):

```
▾ i18n/
  ▾ en/
      app.xml
  ▾ zh/
      app.xml
▸ Resources/
```

两个app.xml 的文件内容都是一样的(目的是,不管是英文的操作系统,还是中文的,都显示一个标题):

```xml
<resources>
  <string name="appname">Ti中国社区</string>
</resources>
```

## 修改启动图

我们替换原来的图片：

- /Resources/android/default.png
- /Resources/iphone 目录下的所有 Default*.png 文件

可以把 /Resources/android/images 删掉.我们没必要对不同的屏幕尺寸增加不同的启动图.


替换成新的文件即可：

![启动图](/images/basic_tutorial_qidongtu.png)

注意：

- 尺寸必须与原来的尺寸一样，例如： /Resources/iphone/Default.png 的尺寸是
320x480, 则新的图片，必须尺寸也是一样。
再如， /Resource/iphone/DefaultPortrait.png 的尺寸是768 x 1024, 则新图片的
尺寸也必须一样。

否则编译可能不会通过。


## 最终效果

![效果](/images/basic_tutorial_complete_app.gif)
