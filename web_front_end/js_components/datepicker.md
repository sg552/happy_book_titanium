#datepicker



##bootstrap-datepicker

>项目地址:https://github.com/eternicode/bootstrap-datepicker

bootstrap本身自带的日期选择器,如下图的展示效果。

![datepicker](/images/datepicker.png)

###使用:
用`rails app`来举例:

>前三步都是在引入bootstrap,最后一步才是使用。

>下载的bootstrap.min.js和 bootstrap.js是一样的效果,只是前者是经过压缩了的,下面同理。

- 在*app/assets/javascripts*下download `bootstrap.js`或`bootstrap.min.js`文件

```console
wget https://github.com/twbs/bootstrap/blob/master/dist/js/bootstrap.js
```

- 在*app/assets/stylesheets*下download `bootstrap.css`或`bootstrap.min.css`文件

```console
wget https://github.com/twbs/bootstrap/blob/master/dist/css/bootstrap.css
```

- *app/assets/javascripts/application.js*中添加如下代码

```javascript
//= require jquery
//= require bootstrap.min
```
- 在*app/views/welcome/index.html.erb* 添加如下代码:

```html
<input type="text" class="datepicker"/>
<script>
  $(function () {
    $('.datepicker').datepicker();
  })
</script>
```
这时候刷新页面,时间选择器应该就出现了。

##bootstrap-datetimepicker

有时候需要时间日期选择器的时候,上面的不够用了。不过有很多前辈已经给了我们做好了,搜索datetimepicker能够出现一大堆。

下面我们举一个例子来使用一下吧:

>项目地址: https://github.com/smalot/bootstrap-datetimepicker

效果图如下:

![datepicker](/images/datetimepicker.png)


- 下载 bootstrap-datetimepicker.min.js 到*app/assets/javascripts*目录下面:

```console
wget https://github.com/smalot/bootstrap-datetimepicker/blob/master/js/bootstrap-datetimepicker.min.js
```

- 下载 bootstrap-datetimepicker.min.css到*app/assets/stylesheets*目录下面:

```console
wget https://github.com/smalot/bootstrap-datetimepicker/blob/master/css/bootstrap-datetimepicker.min.css
```

- 在*app/assets/javascripts/application.js*中添加:
```javascript
 //= require bootstrap-datetimepicker.min
```
 
- 在*app/assets/stylesheets/application.css*中添加:
- 
```css
*= require bootstrap-datetimepicker.min
```
 
- 在*app/views/welcome/index.html.erb* 添加如下代码:

```html
<input type="text" id="datetimepicker"/>
<script>
  $('#datetimepicker').datetimepicker({
    format: 'yyyy-mm-dd hh:ii'
  });
</script>         
```
> 如果需要了解更多的参数或者国际化等,请查看项目地址的详细参数配置。