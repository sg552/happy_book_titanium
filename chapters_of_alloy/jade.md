#jade
jade是什么？

jade是通过javascript实现的用于node的高性能模版引擎。

##安装
```
$ npm install jade (-g)
```

##语法
jade是以空格或缩和换行来实现代码格式，每行的第一个单词都会认为是一个tag。

以传统的html代码和jade代码做比较：

jade代码

```jade
doctype html
html(lang="en")
  head
    title= pageTitle
    script(type='text/javascript').
      if (foo) bar(1 + 5)
  body
    h1 Jade - node template engine
    #container.col
      if youAreUsingJade
        p You are amazing
      else
        p Get on it!
      p.
        Jade is a terse and simple templating language with a
        strong focus on performance and powerful features.
```
这段jade代码可以转换成如下的html代码：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Jade</title>
    <script type="text/javascript">
      if (foo) bar(1 + 5)
    </script>
  </head>
  <body>
    <h1>Jade - node template engine</h1>
    <div id="container" class="col">
      <p>You are amazing</p>
      <p>Jade is a terse and simple templating language with a strong focus on performance and powerful features.</p>
    </div>
  </body>
</html>

```
我们在使用alloy框架开发titanium应用的时候，视图层需要使用xml文件，我们可以比较一段jade文件，和编译后生成的xml文件。

jade 文件
```html
Alloy
    Window
        ScrollableView#scrollableView( showPagingControl="true" width="100%")
            View#view1(backgroundColor="#123")
                ImageView(image="/images/index/guide01.png" width="100%" height="100%" left="%0" top="%0")
            View#view2(backgroundColor="#246")
                ImageView(image="/images/index/guide02.png" width="100%" height="100%" left="%0" top="%0")
            View#view3(backgroundColor="#48b")
                ImageView(image="/images/index/guide03.png" width="100%" height="100%" left="%0" top="%0")
            View#view4
                ImageView(image="/images/index/guide04.png" width="100%" height="100%" left="%0" top="%0")
                Button#go(onClick="go_login") 立即体验
```

xml 文件
```html
<Alloy>
  <Window>
    <ScrollableView id="scrollableView" showPagingControl="true" width="100%">
      <View id="view1" backgroundColor="#123">
        <ImageView image="/images/index/guide01.png" width="100%" height="100%" left="%0" top="%0"></ImageView>
      </View>
      <View id="view2" backgroundColor="#246">
        <ImageView image="/images/index/guide02.png" width="100%" height="100%" left="%0" top="%0"></ImageView>
      </View>
      <View id="view3" backgroundColor="#48b">
        <ImageView image="/images/index/guide03.png" width="100%" height="100%" left="%0" top="%0"></ImageView>
      </View>
      <View id="view4">
        <ImageView image="/images/index/guide04.png" width="100%" height="100%" left="%0" top="%0"></ImageView>
        <Button id="go" onClick="go_login">立即体验</Button>
      </View>
      </ScrollableView>
  </Window>
</Alloy>

```

这里我们可以看出，jade它只需要写出前标签，不用写后标签，以严格的缩进来控制代码的层级，这样我们节约我们的时间来专注于代码内容上了。
