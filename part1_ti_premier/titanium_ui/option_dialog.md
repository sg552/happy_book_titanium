#OptionDialog

**OptionDialog**是Titanium UI Dialog对话框种类中的一种，另一种是你已经在[2.8.5](/alert_dialog.md)章节已经接触过的
AlertDialog。事实上，这两者很像，它们的搭建原理基本相同，只是UI层面上的样式发生一些变化而已；另外在不同的系统平台
上也稍微有些变化。下面是API给出的UI效果参考图：

<table>
  <tr>
    <td>Android</td>
    <td>iPhone</td>
    <td>iPad</td>
    <td>Mobile Web</td>
  </tr>

  <tr>
    <td>
      <img src="http://docs.appcelerator.com/platform/latest/images/optiondialog/optiondialog_android.png"/>
    </td>

    <td>
      <img src="http://docs.appcelerator.com/platform/latest/images/optiondialog/optiondialog_iphone.png"/>
    </td>

    <td>
      <img src="http://docs.appcelerator.com/platform/latest/images/optiondialog/optiondialog_ipad.png"/>
    </td>

    <td>
      <img src="http://docs.appcelerator.com/platform/latest/images/optiondialog/optiondialog_mobileweb.png"/>
    </td>
  </tr>
</table>

#####**Android/Mobile Web**
OptionDialog在Android平台上，明显的和其他三个平台有着显著的区别。在Android系统上，OptionDialog出现在屏幕的中央；
并且每个option选项类似以单选框的形式来进行选择，并存在**默认选择项**。Mobile Web平台上，OptionDilaog则像是一堆
按钮button的组合，出现的位置也是在屏幕的中央。

#####**iPhone/iPad**
在iPhone和iPad平台上，OptionDialog样式区别不大，有三点稍微不同：首先，在iPhone上是有**取消选项Cancel
**的，而iPad却没有取消选项(iPad通过点击OptionDialog其他区域来取消OptionDialog)；除此之外，
iPhone对于取消选项特别的分离显示出来了；最后，在iPhone上OptionDilaog显示在屏幕的底部，而iPad平台上OptionDialog
则和Android平台一样显示在屏幕的中央。

OptionDialog存在**选项操作**，那么我们该如何对我们所做出的“选项”进行确认处理呢？下面我们通过演示案例来详细的介绍
OptionDialog选项的功能处理以及一些重要的属性。下面是演示案例效果图(案例以iPhone平台为基础包含代码)：

![](/images/option_dialog.gif)

_.xml_：
```xml
<Button id='delete_btn' onClick='show_option_dialog'/>

<OptionDialog id='option_dialog' onClick='option_check'>
 <Options>
   <Option color='red'>Confirm</Option>
   <Option color='green'>查看</Option>
   <Option color='blue'>Cancel</Option>
 </Options>
</OptionDialog>
```

_.tss_：
```tss
"#delete_btn":{
  top:'10%',
  width:'20%',
  height:'5%',
  title:'删除'
}

"#option_dialog":{
  width:'95%',
  height:'26%',
  cancel:'2',
  persistent:false,
  destructive:'0',
  opaquebackground:true,
  title:'确定删除文件吗？'
}
```

_.js_：
```js
function show_option_dialog(){
  $.option_dialog.show();
}

function option_check(e){
  if(e.index == 0){
    alert('删除文件');
  }
  else if(e.index == 1){
    alert('查看文件');
  }
  else if(e.index == 2){
    alert('取消删除');
  }
}
```

首先我们可以看到，我们可以在.xml文件使用**OptionDialog**和**options/option**标签来静态定义，动态定义也能达到一样的效果。下面是动态定义的参考代码：

```js
var option_dialog = Ti.UI.createOptionDialog({
  width:'95%',
  height:'26%',
  cancel:'2',
  persistent:false,
  destructive:'0',
  opaquebackground:true,
  title:'确定删除文件吗？',
  options:['Confirm','查看','Cancel']
});
```

对于OptionDilaog的选项处理，我们可以在.xml/.js文件中看出这个点击事件处理是添加在OptionDilaog上的，即直接作用于OptionDilaog而不是作用于每一个选项上。
那么OptionDilaog是如何识别每一个选项的点击处理的呢？答案仍然是通过事件参数e来解决这个问题，从这几章的介绍我们可以看出如果需要通过点击事件来定位页面
中的某个UI控件，或者得到某个父级UI中的子级UI控件或属性的时候，我们都应该考虑是否可以通过事件参数e来解决。在这个演示案例中，我们使用了**e.index**来解
决这个问题，这个index是什么呢？这个index事实上就是option的序号，或者可以说是在父级属性Options下的子级序号；如果还是不太理解我们从动态定义的代码中就应
该明白**options:['Confirm','查看','Cancel']**，即option实际上就是options数组中的元素。所以通过option的index来得到每个option是可以的。

我们明白了选项的处理问题，那么接下来我们看看OptionDilaog几个比较重要的属性：

① **cancel**：这个属性的用来定义OptionDilaog的**取消选项**，它的值为其option的index。

② **persistent**：这个属性用来定义当应用处于**暂停paused**或**挂起suspened**时，OptionDilaog是否继续显示；它的值为boolean值，在演示
案例中我们将这个值设为了**false**，所以当我们通过**home**键跳转到Home页面再返回来是OptionDilaog被取消隐藏了就是这个原因。

③ **destructive**：这个属性用来定义OptionDilaog是一个点击选项操作完毕后“自销毁”的UI控件(即选项操作或点击空白处取消隐藏属性)，本身无
实际意义。它的默认值是**-1**，可设定值为**0**；两者的区别在于当值设置为0时，确认选项的字体颜色会变为**红色**。

④ **title**：定义OptionDilaog的标题。用来描述选项操作的目的。

了解了这些重要的属性和方法，我们就可以熟练的运用OptionDilaog来解决实际的UI需求。如果，你需要更加详细的了解请访问官方给出的API地址：http://docs.appcelerator.com/platform/latest/#!/api/Titanium.UI.OptionDialog-property-destructive
