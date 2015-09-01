# Alloy Widgets 


## widgets介绍


 **Alloy Widgets** 是 **Alloy** 框架的一部分重要功能,封装好的 **Widgets** 能够被多个页面和多个应用来使用。有些类似于封装好的*SDK*,能够提高代码的重用性。


## 如何使用widgets

在开始生成一个新的项目的时候 **Ti** 会自动帮我们创建一个 `app/views` `app/controllers` `app/styles` 目录，用于存储 `MVC` 框架对应的文件。 **Widgets** 是属于 **Alloy** 框架的内容，因此我们需要在 `app` 目录下手动创建 `app/widgets` 目录。

* 复制 `com.example.widget(自定义的widget名字)` 到新创建的 `app/widgets` 目录下面。如下图所示:
    
  ```
app
├── config.json
├── controllers
│   └── index.js
├── views
│   └── index.xml
└── widgets
    └── com.example.widget
        ├── controllers
        │   ├── foo.js
        │   └── widget.js
        ├── views
        │   ├── foo.xml
        │   └── widget.xml
        └── widget.json
  ```
* 在 `app/config.json` 文件里面的 `dependencies` 属性里面声明 *widget* 的 `name` 和 `version` 的键值对:

  ```
{
		...
   		"dependencies": {
    		"com.example.widget":"1.0",
		}
}
  ```
* 在需要引用 `widgets` 的地方应用 `com.example.widget` 。
  * 在 *Alloy View* 中的引用 *widget* 方式:

  ```
app/views/index.xml
<Alloy>
    	<Window>
       		<Widget src="com.example.widget" id="foo" name="foo" />
    	</Window>
</Alloy>
  ```

  * 在 *controller* 中的引用 *widget* 方式。

  ```
widget = Alloy.createWidget('com.example.widget', {
		'title' : 'new_title'
});
  ```
  
## 如何创建一个widget


 **Widgets** 作为组件在程序启动时自动加载，内置 *view* , *style* , *controller* , *models* , *theme* , *assets* , *libs* 等等。因此，*view* 视图, *controller* 里面的 `function` , *style* 里面的 *tss* 样式等都能够被重复使用。
 
### widgets 与 alloy 的区别 
  * *widget.js* , *widget.tss* , *widget.xml* 代替默认的 *index.js* , *index.tss* , *index.xml*
  * 使用`app/widgets/foo/lib/helper.js`时需要`require(WPATH('helper')) `
  * 使用`app/widgets/foo/assets/images/foo.png`时需要`WPATH('images/foo.png')`
  * 有单独的配置文件 *widget.json* 代替 *config.json*
### TODO 创建widget


## widgets 的特性

* **widget** 自身能够调用其他的 **wiget** 
* 支持 **alloy** 自身的特性
* 重用性和移植性强

## widgets库
* **Titanium** 官方提供一些 **Widgets**
* **http://gitt.io** 有许多 **Wigets** 和 **modules**
 


