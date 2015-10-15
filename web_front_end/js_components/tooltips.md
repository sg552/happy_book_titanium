# Tooltips(提示框)

##jquery Tooltips

> 项目地址: https://jqueryui.com/tooltip/

使用jquery给输入框组件增加提示方式非常简单

- 引用`jquery`相关的js和css文件
- 在`script`中使用

	```
	$(function() {
    	$( document ).tooltip();
   });
	```
- 给`input`加入`title`属性就可以了

下面是一个小的例子:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <link rel="stylesheet" href="http://code.jquery.com/ui/1.11.4/themes/smoothness/jquery-ui.css">
  <script src="http://code.jquery.com/jquery-1.10.2.js"></script>
  <script src="http://code.jquery.com/ui/1.11.4/jquery-ui.js"></script>
  <script>
  $(function() {
     $( document ).tooltip();
  });
  </script>
</head>
<body>
	<input title="我是一个提示框">
</body>
</html>
```
提示框效果图如下:

![tooltips_left](/images/tooltips.gif)

##Bootstrap Tooltips

> ref: http://getbootstrap.com/javascript/#tooltips

效果图:

![tooltips_left](/images/tooltips_left.png)
	
![tooltips_right](/images/tooltips_right.png)

- 导入bootstrap,用[Tabs](tabs.html)(	标签页)中的导入方式

- 在页面中添加代码如下即可:

```html
<h1 style="margin-bottom: 50px;">bootstrap tooltips</h1>

<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="left" title="Tooltip on left" style="margin-left: 50px;">Tooltip on left</button>
<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="top" title="Tooltip on top">Tooltip on top</button>
<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="bottom" title="Tooltip on bottom">Tooltip on bottom</button>
<button type="button" class="btn btn-default" data-toggle="tooltip" data-placement="right" title="Tooltip on right">Tooltip on right</button>
<script>
  $(function () {
    $('[data-toggle="tooltip"]').tooltip()
  })
</script>
```