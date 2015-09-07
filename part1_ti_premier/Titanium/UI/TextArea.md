# Titanium.UI.TextArea

>        此处用的Titanium官方的图片和例子

![android](http://docs.appcelerator.com/platform/latest/images/textarea/textarea_android.png)  | ![ios](http://docs.appcelerator.com/platform/latest/images/textarea/textarea_ios.png) | ![mobileweb](http://docs.appcelerator.com/platform/latest/images/textarea/textarea_mobileweb.png)  |
------------- | ------------- | ------------- |
android  | ios | mobileweb |



在controller中创建textarea的例子:

*app/controllers/textarea.js*

```javascript
 var win = Ti.UI.createWindow({
   backgroundColor: 'white'
 });

 var textArea = Ti.UI.createTextArea({
    borderWidth: 2,
    borderColor: '#bbb',
    borderRadius: 5,
    color: '#888',
    font: {fontSize:20, fontWeight:'bold'},
    keyboardType: Ti.UI.KEYBOARD_NUMBER_PAD,
    returnKeyType: Ti.UI.RETURNKEY_GO,
    textAlign: 'left',
    value: 'I am a textarea',
    top: 60,
    width: 300, height : 70
 });

 win.add(textArea);

 win.open();
```


在view中创建textarea的例子:

*app/views/index.xml*

```xml

<Alloy>
   <Window id="win" backgroundColor="white">
       <TextArea id="textArea"  borderWidth="2" borderColor="#bbb" borderRadius="5"
           color="#888" textAlign="left" value="I am a textarea"
         top="60" width="300" height="70" />
   </Window>
</Alloy>

```
