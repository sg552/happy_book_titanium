# 标签

一个jQuery UI插件，来处理多标签字段。

## 使用方法

### 添加jQuery和jQuery UI插件：

```
<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.5.2/jquery.min.js" type="text/javascript" charset="utf-8"></script>
<script src="https://ajax.googleapis.com/ajax/libs/jqueryui/1.8.12/jquery-ui.min.js" type="text/javascript" charset="utf-8"></script>
<script src="js/tag-it.js" type="text/javascript" charset="utf-8"></script>
```

### 添加样式文件：

```
<link rel="stylesheet" type="text/css" href="http://ajax.googleapis.com/ajax/libs/jqueryui/1/themes/flick/jquery-ui.css">
<link href="css/jquery.tagit.css" rel="stylesheet" type="text/css">
```

### 一个helloword：

```
<script type="text/javascript">
  $(document).ready(function() {
      $("#tags").tagit();
      });
</script>

<ul id="tags">
  <li>Tag1</li>
  <li>Tag2</li>
</ul>
```

## demo和方法:

### 自动补全功能：

- 用数组的方式，设置可选值：
```
$("#tags").tagit({
    availableTags: ["ios", "java", "php", "javascript", "ruby", "python", "c"]
    });
```

- 自定义自动补全：
```
$(function() {
  var availableTags = ["asp", "ajax", "java", "javascript", "php", "ruby", "python"];
  $("#tags").autocomplete({
    source: availableTags
  });
});
<input id="tags">
</input>
```

### removeConfirmation (boolean)

```
$('#removeConfirmationTags').tagit({
  availableTags: availableTags,
  removeConfirmation: true
});

```

### read-only tag
```
$('#readOnlyTags').tagit({
  readOnly: true
});
```

### method-tag

```
$('#methodTags').tagit({
  availableTags: availableTags
});
```

### event-tag

```
var eventTags = $('#eventTags');
var addEvent = function(text) {
  $('#events_container').append(text + '<br>');
};
```

### allow spaces without quote

```
$('#allowSpacesTags').tagit({
  availableTags: availableTags,
  allowSpaces: true
});
```

更多示例请参考：http://aehlke.github.io/tag-it/examples.html












