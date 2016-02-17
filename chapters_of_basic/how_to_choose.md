# 如何考察一门新技术

在软件开发中，学习一种新语言/框架/技术 的成本很高。而且往往它们有多个同类
的竞争对手，我们该如何选择呢？

原则：先多了解（花上3~5天)， 再亲手试一下，写个hello world.

下面以Titanium 为例，我是如何选择到它的呢？

作为一名ruby/java背景的web开发者，我完全受不了原生的移动开发。在之前我是
知道jruby的（ruby代码可以完美运行于JVM环境中），所以，想，如果有一种技术
可以这样做就好了。

于是就搜索 "ruby android" .

然后就发现了 ruboto, rubymotion.  ruboto 就是ruby on Android, rubymotion
当时是 ruby on iOS. (当时是2014年9月左右, 现在rubymotion已经支持了android）

然后，多了解下rubymotion(阅读stackoverflow上的文章), 发现了其他的同类产品：

Xamarin, phonegap.

找到官方网站，依次阅读 tutorial ，发现Xamarin 是用C#做的跨平台开发工具，跟
rubymotion和Titanium特别相似。可惜我的技术背景不是C#，所以就没考虑。

phonegap 属于 hybrid开发, 随便一搜发现大家吐槽它的太多。开发是快，但是用户
体验极差，卡的要死，没法跟原生app相比。 而且支持原生的功能有限。（在当时
PUSH啊，重力感应啊，底层接口啊都几乎没有支持） 所以我就放弃了。

搜索phonegap的时候， 输入 phonegap, xamarin时， 发现有个文章中又提到了titanium.
于是就深入了解。发现它正是我想要的：

- 一套代码，解决多个平台
- 生成的原生代码速度极快
- Alloy框架实现了MVC分离，可读性极强。
- 能很好的支持native code。

所以就选了它。

第二备选是 rubymotion.

