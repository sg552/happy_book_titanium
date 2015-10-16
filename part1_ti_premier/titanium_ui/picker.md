#Picker
**Picker**是Titanium提供的一个“**点击下拉选择**”UI组件，不过这并不是它唯一的效果，它还有一种效果是不通
过“点击下拉”选择操作来选择而是通过“**滑动**”选择来操作。这种区别在Android平台上都可以展示出来，而
IOS平台则不行，因为Picker在IOS平台上只有“滑动”选择这一种操作。在Android平台上这种不同选择操作效果的实现
可以通过属性**useSpinner**来控制，我们下面会详细介绍。以下是Picker的UI展示效果图(包含实现代码)：

<table>
  <tr>
    <td>Android</td>
    <td>IOS</td>
  </tr>

  <tr>
    <td>
      <img src="/images/picker_android.gif"/>
    </td>

    <td>
      <img src="/images/picker_ios.gif"/>
    </td>
  </tr>
</table>

以下是Android平台上UI效果的实现代码，IOS平台实现代码与此相同，不需要设置属性**useSpinner**属性即可。

_**.xml**_
```xml
<Picker class='picker_android' top='45%' left='10%'>
  <PickerColumn>
     <PickerRow title="data 1"/>
     <PickerRow title="data 2"/>
     <PickerRow title="data 3"/>
     <PickerRow title="data 4"/>
  </PickerColumn>
</Picker>

<Picker class='picker_android' useSpinner='true' top='38%' right='10%'>
  <PickerColumn>
     <PickerRow title="data 1"/>
     <PickerRow title="data 2"/>
     <PickerRow title="data 3"/>
     <PickerRow title="data 4"/>
  </PickerColumn>
</Picker>
```
演示案例代码：
```xml
<Picker id='picker' change='picker_check'>
 <PickerColumn id='picker_column1'/>
 <PickerColumn id='picker_column2'/>
</Picker>
```

```js

```
