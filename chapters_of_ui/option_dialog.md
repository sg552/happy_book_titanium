# OptionDialog

OptionDialog对话框种类中的一种，另一种是[Alert Dialog](/chapters_of_ui/alert_dialog.md)
中已经接触过的 AlertDialog。事实上，这两者很像，它们的搭建原理基本相同，
只是UI层面上的样式发生一些变化而已；另外在不同的系统平台
上也稍微有些变化。

![android](/images/ui_optiondialog_android.png) | ![iphone](/images/ui_optiondialog_iphone.png) | ![ipad](/images/ui_optiondialog_ipad.png)
:---:|:---:|:---:
android | iPhone | iPad

在Android系统上，OptionDialog出现在屏幕的中央；
并且每个option选项类似以单选框的形式来进行选择，并存在默认选择项
selectedIndex(只适用于Android)。

在iPhone和iPad平台上，OptionDialog样式区别不大，有三点稍微不同：

- 在iPhone上是有取消选项Cancel的，而iPad却没有取消选项(通过点击
其他区域来取消)；
- iPhone对于取消选项特别的分离显示出来了；
- 在iPhone上, OptionDilaog显示在屏幕的底部，iPad平台上显示在屏幕的中央。

OptionDialog存在选项操作，那么我们该如何对我们所做出的“选项”进行确认处理呢？下面我们通过演示案例来详细的介绍
OptionDialog选项的功能处理以及一些重要的属性。下面是演示案例效果图(案例以iPhone平台为基础包含代码)：

![option_dialog](/images/ui_optiondialog.png)

## 使用

```js
var win = Ti.UI.createWindow();
win.backgroundColor = 'white';

var option_dialog = Ti.UI.createOptionDialog({
  width:'95%',
  height:'26%',
  cancel:'2',
  persistent:false,
  destructive:'0',
  opaquebackground:true,
  title:'确定删除文件吗？',
  options:['确定','查看','取消']
});

// 点击window 任意部位，就可以弹出这个会话框:
win.addEventListener('click', function(){
  option_dialog.show();
})
win.open();
```

对于OptionDilaog的选项处理，我们可以看出这个点击事件处理是添加在
OptionDilaog上的，即直接作用于OptionDilaog而不是作用于每一个选项上。
那么OptionDilaog是如何识别每一个选项的点击处理的呢？答案仍然是通过事件参数e
来解决这个问题。

从这几章的介绍我们可以看出如果需要通过点击事件来定位页面
中的某个UI控件，或者得到某个父级UI中的子级UI控件或属性的时候，
我们都应该考虑是否可以通过事件参数e来解决。

在这个演示案例中，我们使用了e.index，这个index是什么呢？就是option的序号，
或者可以说是在父级属性Options下的子级序号；
`options:['确定','查看','取消']`，
即option实际上就是options数组中的元素。
所以通过option的index来得到每个option是可以的。

我们明白了选项的处理问题，那么接下来我们看看OptionDilaog几个比较重要的属性：

- cancel
用来定义OptionDilaog的取消选项，它的值为其option的index；
被定义之后取消选项Cancel会被突出而分离出来。

- persistent
用来定义当应用处于暂停paused或挂起suspened时，OptionDilaog是否继续显示；
它的值为boolean，在演示中我们将这个值设为了false，

- destructive
用来定义OptionDilaog是一个点击选项操作完毕后“自销毁”的UI控件
(即选项操作或点击空白处取消隐藏属性)，本身无实际意义。
默认值是-1，可设定值为0；两者的区别在于当值设置为0时，
确认选项的字体颜色会变为红色。

- title
定义OptionDilaog的标题。用来描述选项操作的目的。

了解了这些重要的属性和方法，我们就可以熟练的运用OptionDilaog来解决实际的
需求。
