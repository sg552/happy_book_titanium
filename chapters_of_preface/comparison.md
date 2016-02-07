# titanium 与 native app的执行效率对比。

下图是 titanium 的运行机制，我们可以看出，所有的js代码，都是
在 java v8或者 object c 中的JavascriptCore 环境中运行的。

![titanium_mobile_runtime](/images/titanium_mobile_runtime.jpg)

所以，基本上，我们可以从这个层面看到精确的数值。

