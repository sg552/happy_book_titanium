#Titanium.UI.iOS.CoverFlowView
cover flow view是一个用于3d动画展示图片的容器。

创建的话可以使用`Titanium.UI.iOS.createCoverFlowView`或者在Alloy框架中的xml文件中使用`<CoverFlowView>`标签对。

##例子
创建一个包含三张图片的简单cover flow的例子
```javascript
var view = Titanium.UI.iOS.createCoverFlowView({
    backgroundColor:'#000',
    images:['a.png','b.png','c.png']
});
window.add(view);
```

在Alloy的xml文件中实现上面同样的效果：
```xml
<Alloy>
    <Window id="window">
        <CoverFlowView id="view" platform="ios" backgroundColor="#000">

            <!-- The Images tag sets the CoverFlowView.images property. -->
            <Images>

                <!-- Assign the image by node text or the image attribute. -->
                <!-- Can also specify the width and height attributes. -->

                <Image>a.png</Image>
                <Image>b.png</Image>
                <Image>c.png</Image>

            </Images>

            <!-- Place additional views for the CoverFlowView here. -->

        </CoverFlowView>
    </Window>
</Alloy>
```
