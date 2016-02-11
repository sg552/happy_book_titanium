# Picker

Picker 选择框。

![android](/images/ui_picker_android.gif) | ![ios](/images/ui_picker_ios.gif)
:---:|:---:
Android | iOS

在安卓上有下拉和滑动两种效果，ios上只有滑动一种效果。

在Android平台上不同选择效果的实现可以通过属性useSpinner来控制。

以下是Android平台上UI效果的实现代码，IOS平台实现代码与此相同，
不需要设置属性useSpinner属性即可。

## 例子

```js

var win = Ti.UI.createWindow();
win.backgroundColor = 'white';

var picker = Ti.UI.createPicker({
  top: 50
})

var data = [];
data[0] = Ti.UI.createPickerRow({title: '星期一'});
data[1] = Ti.UI.createPickerRow({title: '星期二'});
data[2] = Ti.UI.createPickerRow({title: '星期三'});
data[3] = Ti.UI.createPickerRow({title: '星期四'});

picker.add(data);
picker.selectionIndicator = true;

win.add(picker);

win.open();

```

## 日期选择框

![date picker](/images/ui_picker_date.png)

```js

var win = Ti.UI.createWindow();
win.backgroundColor = 'white';

picker = Ti.UI.createPicker({

  type: Ti.UI.PICKER_TYPE_DATE,
  minDate: new Date(2012,1,1),
  maxDate: new Date(),   // 当前日期
  value: new Date(),
  top: 50
})

win.add(picker);
win.open();

picker.addEventListener('change', function(e){
  console.info('您选择了：' + e.value);
});

```

选择后，控制台会输出：

```
[INFO]  您选择了：Thu Apr 11 2013 00:00:00 GMT+0800 (CST)
[INFO]  您选择了：Sat Apr 13 2013 00:00:00 GMT+0800 (CST)
```

## 重要属性

### type

定义了picker的类型，目前有几种：

- Ti.UI.PICKER_TYPE_COUNT_DOWN_TIMER: 倒计时，仅用于ios.
- Ti.UI.PICKER_TYPE_DATE: 日期
- Ti.UI.PICKER_TYPE_TIME: 时间
- Ti.UI.PICKER_TYPE_DATE_AND_TIME: 日期和时间
- Ti.UI.PICKER_TYPE_PLAIN: 普通选项（默认）

### useSpinner

使用 滑动式 选择框，仅用于 Android.  Android的选择框默认是下拉单形式的。

使用多列选择框时，这个属性必须是 true

- true
- false（默认）

### 多列选择框

很多时候我们要用多列选择框，例如，选择 "省-市-区-县"，
或者选择"一级-二级-三级" 菜单。

![多列选择框](/images/ui_picker_multiple_columns.png)

这时我们要使用PickerRow和 PickerColumn了。如下

```js
var win = Ti.UI.createWindow();
win.backgroundColor = 'white';

picker = Ti.UI.createPicker({
  top: 50,
  useSpinner: true
})
picker.selectionIndicator = true;

var provinces = ['辽宁省', '西藏', '海南省'];
var cities = ['沈阳市', '拉萨市', '三沙市'];

var province_column = Ti.UI.createPickerColumn();
for( var i =0; i < provinces.length; i++){
  var row = Ti.UI.createPickerRow({
    title: provinces[i]
  });
  province_column.addRow(row);
}

var city_column = Ti.UI.createPickerColumn();
for( var i =0; i < provinces.length; i++){
  var row = Ti.UI.createPickerRow({
    title: cities[i]
  });
  city_column.addRow(row);
}

picker.add([province_column, city_column]);

win.add(picker);
win.open();

picker.addEventListener('change', function(e){
  console.info(JSON.stringify(e));
});
```

### 如何获取选择到的值？

有两种方式：

- 对于日期/时间，直接使用 e.value
- 对于非日期型选择框，要使用"change/click"事件的属性：
  - selectedValue: 选择框中的值，例如： ["海南省", "三沙市"]
  - rowIndex: 该事件发生于哪一行，例如：0
  - columnIndex: 该事件发生于哪一列，例如：1

例如，下面代码就是在上面例子中，用户点击任一一个选择框之后，打印出来的事件：

```js
//注意下面三行代码
picker.addEventListener('change', function(e){
  console.info(JSON.stringify(e));
});
```

格式化后的JSON结果, 可以看到里面的 columnIndex, rowIndex 以及 selectedValue：

```json
{
   "row":{
      "horizontalWrap":true,
      "visible":true,
      "title":"三沙市"
   },
   "rowIndex":2,
   "selectedValue":[
      "海南省",
      "三沙市"
   ],
   "columnIndex":1,
   "column":{

   },
   "bubbles":true,
   "type":"change",
   "source":{
      "type":-1,
      "horizontalWrap":true,
      "visible":true,
      "top":50,
      "useSpinner":true,
      "selectionIndicator":true,
      "columns":[
         {
         },
         {
         }
      ]
   },
   "cancelBubble":false
}
```
