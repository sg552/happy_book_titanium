# 移动端的中间件

我们的WEB开发，遵循着HTML规范。 我们的浏览器都能直接解析HTML语言。所以
我们修改某个HTML页面时，直接修改文本文件就行了。

不会出现要把 HTML 页面进行编译的情况。

如果移动端也有这样的中间件（例如nginx, apache 或者 客户端的 browser ）
那么绝对是一场变革。

举个例子：

下面的代码，可以直接输出一个html页面：

```
<html>
  <body>
    <p>hello, world</p>
  </body>
</html>
```

如果有这样的文件，我直接修改，不需要打包，编译，用某种办法弄到手机上，
并且马上生效。 那就太棒了。

TODO 补上图片。  上层是代码，中间是中间件，下层是操作系统。

这篇文章： http://mobile.51cto.com/news-491790.htm
从中间件的历史来看移动App开发的未来  说的非常好。
