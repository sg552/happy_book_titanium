# titanium 与 native app的执行效率对比。

下图是 titanium 的运行机制，我们可以看出，所有的js代码，都是
在 java v8或者 Object C 中的JavascriptCore 环境中运行的。

可以说，V8有多快，Titanium就有多快！

![titanium_mobile_runtime](/images/titanium_mobile_runtime.jpg)

在人肉体验上讲, Titanium 跟native app的运行速度是一样的。人肉基本体会不到
Titanium 的应用有卡顿感。

