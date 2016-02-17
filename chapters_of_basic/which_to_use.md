# 哪些用，哪些不用。

对于Titanium的定位，我认为是 快速开发原型。验证可行性。所以只考虑公司一年内
的发展情况即可。

## 只用Titanium SDK

考虑到国内的 GFW，国外很多服务是用不了的，比如google map, google play, 所以
我们就要用本土的东西。

- 不用国外的push服务。
- 不用国外的聊天服务。
- 不用Appcelerator 自带的云服务。
- 不用Dashboard. （统计等等）

这些在国内都有替代品。

## 不用 alloy

alloy 的理念很先进，也是当初我做技术选型时选择Titanium的主要原因。不过经过
若干项目的实践，我们发现几个致命弱点：

- 编译时间久。 我们的项目后期编译一次都需要20秒了。这段等待时间足够让大家
的思路断掉。

- 编译出来的代码难以调试。 由于alloy 相当于是你的代码和 Titanium代码的一个
中间层，所以alloy中出现的问题不会很直观的在 console log中得到体现。比如，
alloy中如果使用 数字 作为某个元素的id ，titanium 就会报错。并且出错的信息
根本就与实际的错误原因无关。

- Alloy 使用了DSL。非常清晰明白，让人一看就懂。但是缺点也在这里，
初学者一旦习惯了Alloy( xml + tss + js)，往往不愿意读 传统移动开发的代码(
视图，样式和逻辑混合写在一起的js) 。

现在无论是android 还是ios 开发，都是后一种形式的操作。所以，大家要适应。

- 无法使用自动适配的长度函数. 在Titanium 中，我们可以动态的计算某个元素
的长宽：

```js
Ti.UI.createView({
  width: __l(300);
})
```

这里的 __l()方法就是 专门动态获取屏幕尺寸的函数，我们用这个函数就可以完美
的做到适配多个屏幕。但是在Alloy的 tss中，我们无法这样做。

考虑到这些致命缺点，我建议不要用Alloy。

## 只写android/ios 即可

根据公开数据显示，在中国，2015年6月，Android 市场占有率是 74%，iphone 24.4%,
window phone 占 1%。

所以，如果你的用户量不是BAT那么大的话，没有必要做Windows端。

## 不要用Titanium 写web

H5页面的选择有很多，可以用 react, metoer, angular, vuejs, backbone.

虽然Titanium支持跨平台，但是代码不是100% 复用的。很多代码仅仅android能用，
很多代码仅 ios能用。 根据我们的经验，大约80%的代码通用，20%不通用。

```js
if(is_android){

}else if (is_ios){

}else if (is_mobile_web){

}
```

而且web技术非常普及，开发门槛比 移动app开发要低很多。与其在Titanium的框架内
使用mobile web, 还不如脱离Titanium 直接使用。

出了问题也更加方便排查，项目更容易控制。

## 不要使用官方自带的后端Arrow , 要使用自己的服务器端

原因在于：

1. GFW。 网络的稳定是一切的基础。
2. 官方自带的Arrow后端，实际上是对node的一种封装。 与其学习封装后的东西，
还不如直接学习一个后端语言来的快。

出了问题也好排查。

Ruby on Rails, Python的 Tornado, Django , Php 等等，可供选择的太多了。
没见到 Appcelerator在这方面有优势。

## 不要用Appcelerator Studio

问题还是在网络。

而且，使用命令行可以更好的帮助我们排查问题，加快开发。
