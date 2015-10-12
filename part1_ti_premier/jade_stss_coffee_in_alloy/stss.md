#stss
STSS -- Sassy TSS,or Sassy Titanium Style Sheets.

stss使用的是SCSS(sassy css)的语法
STSS允许你管理SCSS的所有能量来生成你的TSS样式表，内部属性，变量等都可以。

##语法
SCSS是CSS的一个超集。可以直接把CSS并入SCSS文件中。但是，STSS就不是这样，它是直接在SCSS的上层构建的，也就是说STSS是SCSS的超集。它不是在TSS上层构建的，如果你在其中直接参杂TSS的话，则会编译失败。

##安装
安装有两种方法，一个是本地安装，一个是全局安装。如果你要在一个项目中安装stss的话，就可以使用本地安装。如果你希望任何项目都可以使用stss的话，就可以使用全局安装，这样你不需要在开发不同项目时，多次安装stss。

###本地安装
```
npm install stss
```
在安装stss期间，会试图去添加一个预编译的钩子到你的alloy.jmk文件中，如果不存在的话，会创建这个文件。

###全局安装
```
npm install stss -g
```

##用法
STSS可以使用命令行或者直接和api交互使用。如果这个预编译的钩子已经成功安装了，你就不需要再做什么事了。每次你在编译你的app的时候，STSS就会被轻易调用。

###命令行（command line interface）
如果不是在alloy框架下的项目，多数情况下，你只需要使用命令行来把stss加到你的项目中。

把STSS文件转换成TSS文件：
```
stss <input.stss> <output.tss>
```

例如
```
stss stss/app.stss tss/app.tss
```

###API
STSS同样可以被直接与API交互

通过文件路径来引用STSS文件
```css
var stss = require('stss');
stss.render({
    file: stss_filename,
    success: callback
    [, options..]
});
```

也可以直接应用STSS数据
```css
var stss = require('stss');
stss.render({
    data: stss_content,
    success: callback
    [, options..]
});
```

还可以使用```renderSync```方法来执行
```css
var stss = require('stss');
stss.renderSync({
    file: stss_filename,
    success: callback
    [, options..]
});
```

在alloy中使用的例子

stss文件
```css
$red: red;
$green: green;

.message {
  border: 1px solid #ccc;
  padding: 10px;
  color: $red;
}

.success {
  @extend .message;
  border-color: $green;
}
```
会被编译成：
```css
".message": {
  border: "1px solid #ccc",
  padding: "10px",
  color: "red"
},
".success": {
  border: "1px solid #ccc",
  padding: "10px",
  color: "red"
},
".success": {
  borderColor: "green"
}
```

总结：

我们发现在写stss文件的时候：

+ 每行以;结束。

+ 定义的.class，#id前后不需要双引号。

+ 属性的值不需要双引号。

+ 可以定义变量。
