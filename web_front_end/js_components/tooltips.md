# Tooltips(提示框)

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