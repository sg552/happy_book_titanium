# 自定义字体

Titanium 支持`TrueType`和`OpenType`字体（包括iOS和Android）。
需要注意的是，iOS和Android在引用字体的时候有很多不同的地方。

## 字体文件

TTF或者OTF字体都可以被Titanium使用。根据你应用的证书和发布模式，
你可能需要付费才能使用，当然你也可以使用免费的开源字体。

> 找字体可以来这两个站点：Google WebFonts和 FontSquirrel。

## 非Alloy下(经典开发模式)的使用方式

在经典模式下，Titanium的应用需要添加一些运行时平台切换的代码去申请权限。如果要使用自定的字体的话，就按下面来做：

###在经典模式下使用自定义字体 ：

1.准备：把字体文件拷贝到你项目下的`Resources/fonts/`目录。
想在不同的平台上使用不同字的话，分别把文件拷到`Resources/iphone/fonts`和
`Resources/android/fonts`。

2.代码中，设置好`fontFamily`：
```javascript
//假设你要用 "Spicy Rice" ，先下载好 "SpicyRice-Regular.ttf" 文件：

// 为不同的平台设置名字
font_family_name = Ti.Platform.osname=='android' ?
  'SpicyRice-Regular' :   // 这是安卓平台的名字
  'Spicy Rice'            // IOS 平台的名字

var label1 = Titanium.UI.createLabel({
   color:'#000',
   text:'I am Window 1',
   font:{
      fontSize:40,
      fontFamily: font_family_name
   },
   textAlign:'center'
});
```

### iOS平台的注意事项

对于iOS编译的时候，所有放在`Resources/fonts`的文件夹里的字体都会被自动的加进
info.plist文件。

如果你只希望某个字体仅用于android平台, 则字体文件应该放到
`Resources/android/fonts`中。


## Alloy中的使用方式

在Alloy下使用字体的话，在`app/assets/android`或者`app/assets/iphone`
下创建fonts文件夹。例如：

![alloy](/images/senior_customize_font.png)

*app/views/index.xml*:

```xml
<Alloy>
  <View>
      <Label id="spicyrice">This is Spicy Rice.</Label>
      <Label id="burnstowndam">This is Burnstown Dam.</Label>
  </View>
</Alloy>
```

然后再去对应的tss文件中根据id来设置`fontFamily`，要注意的：

- Android在使用的时候，只写文件的名字不写文件的后缀。
- iOS使用的时候，写的是字体的PostScript名（
可以使用Mac上自带的字体册来查看字体的PostScript名）。

由于PostScript名是内置在字体文件里的，即使你修改了字体名字，
也不改变PostScript名。

以Burnstown Dam字体的字体文件为例－－‘burnstown_dam.otf’。
在Android中，你该像下面设置：

```css
"#burnstowndam": {
  font: {
      fontFamily: 'burnstown_dam'
  }
}
```

在iOS中，因为它的PostScript名是‘BurnstownDam-Regular’，所以在 iOS中要这样写：
```css
"#burnstowndam": {
  font: {
      fontFamily: 'BurnstownDam-Regular'
  }
},
/*当你在要兼容两个平台的时候，你的样式文件可以这样写：*/
"#burnstowndam[platform=ios]": {
  font: {
    fontFamily: "BurnstownDam-Regular"
  }
},
"#burnstowndam[platform=android]": {
  font: {
    fontFamily: "burnstown_dam"
  }
}
```

