#ProgressBar
**ProgressBar进度条**是一个用来展示“进度”的UI组件，我们常见的上传或下载进度条都可以通过这个UI组件
来实现(展示进度的另一种方式是使用**ActivityIndicator**，请参考[2.8.3](/activity_indicator.md)小节)。

ProgressBar可以在.xml文件中静态定义，也可以在.js中动态定义；下面给出一个完整的演示参考代码(包括效果图)：

![](/images/progress_bar_display.gif)

_.xml：_
```xml
<Alloy>
    <Window class="container">
        <ProgressBar id="progress_bar"/>
        <Button id='download_btn' onClick='download'/>
    </Window>
</Alloy>
```

_.tss：_
```tss
".container":{
  width:'100%',
  height:'100%',
  backgroundColor:'white'
}

"#progress_bar":{
  font:{
    fontSize:'12'
  },

  top:'5%',
  width:'45%',
  height:'Ti.UI.SIZE',

  min:0,
  max:100,
  value:0,
  color:'red',
  style:Ti.UI.iPhone.ProgressBarStyle.PLAIN
}

"#download_btn":{
  top:'8%',
  width:'20%',
  height:'5%',
  title:'下载'
}
```

_.js：_
```js
var progress_step = $.progress_bar.value;
var timer; //这里为进度的显示设置了一个计时器，是为了让进度增长以0.25速率递增，为了演示而设置没有实际意义；项目中应当以实际的下载进度来设置
var download_flag = true;

function download(){
  if(download_flag){
      if($.download_btn.title == '下载'){
        $.download_btn.setTitle('暂停');
        download_start();
      }
      else if($.download_btn.title == '暂停'){
        $.download_btn.setTitle('下载');
        clearInterval(timer);
      }
  }
  else{
      alert('下载已完成');
  }
}

function download_start(){
  timer = setInterval(function(){
    progress_step++;

    if(progress_step < $.progress_bar.max){
      $.progress_bar.setValue(progress_step);
      $.progress_bar.setMessage(progress_step+'%');
    }
    else if(progress_step == $.progress_bar.max){
      clearInterval(timer);

      $.progress_bar.setMessage('下载完成');
      $.download_btn.setTitle('下载');
      download_flag = false;
    }
  },125);
}

$.index.open();
```

通过上面的演示案例，我们可以梳理出ProgressBar的一些重要属性，下面我们将重点讲述这些属性和
使用方法：

① **min**：定义ProgressBar的最小**初始值**，即进度从哪里开始递增；一般从0开始，也可以设置为其他值，但必须是number型。

② **max**：与min相对应，定义ProgressBar的最大值，当进度为**最大值**时进度递增结束。

③ **value**：ProgressBar的**进度值**，显示当前ProgressBar的进度为多少。

④ **color**：定义ProgressBar的进度值的颜色。

⑤ **style**：ProgressBar的样式类型。在不同的系统平台上，ProgressBar的默认样式不尽相同，

