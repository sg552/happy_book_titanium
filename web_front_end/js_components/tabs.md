#web tabs(标签页)

> ref: http://getbootstrap.com/getting-started/

下面以rails为例子

- 导入bootstrap文件
   
   >这种导入方式是手动导入,没有用gem。你也可以选择用gem导入bootstrap
    
	- 下载[bootstrap](http://getbootstrap.com/getting-started/)的包文件,打开里面的zip包解压查看内容
	- 将里面的*js/bootstrap.min.js*复制到rails项目中*app/assets/javascripts*目录下面
	- 将*css/bootstrap.min/css* *css/bootstrap.theme.min.css*复制到rails项目中*app/assets/stylesheets* 目录下面
	- 将*font*文件夹复制到rails项目的*app/assets*目录下面
	- 在*app/assets/javascripts/application.js* 添加代码:

	```
	//= require bootstrap.min
	```
	- 在*app/assets/stylesheets/application.css* 添加代码:

	```
	*= require bootstrap.min
	*= require bootstrap-theme.min
	```
- 增加一个简单的标签页
	- 添加代码到*app/views/welcome/index.html.erb*中:
	
	```
	<div>
		<ul class="nav nav-tabs">
  			<li class="active"><a href="#">Home</a></li>
  			<li><a href="#">Menu 1</a></li>
  			<li><a href="#">Menu 2</a></li>
  			<li><a href="#">Menu 3</a></li>
		</ul>
	<div>
	```
	
	这时候一个简单的标签页就做好了。如图所示:
	
	![simple_tabs.png](/images/simple_tabs.png)
	
- 有二级选项的标签页
  
  如图所示:
  
  ![tabs.png](/images/tabs.png)
  
  - 添加代码到a*pp/views/welcome/index.html.erb*中:
  
  ```
  <ul class="nav nav-tabs">
  		<li class="active"><a href="#">Home</a></li>
  		<li class="dropdown">
    		<a class="dropdown-toggle" data-toggle="dropdown" href="#">Menu 1
    		<span class="caret"></span></a>
    		<ul class="dropdown-menu">
      			<li><a href="#">Submenu 1-1</a></li>
      			<li><a href="#">Submenu 1-2</a></li>
      		<li><a href="#">Submenu 1-3</a></li> 
    		</ul>
  		</li>
  		<li><a href="#">Menu 2</a></li>
  		<li><a href="#">Menu 3</a></li>
</ul>
  ```