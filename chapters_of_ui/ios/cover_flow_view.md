# CoverFlowView

用于3d动画展示图片的容器。

![cover flow](/images/ui_ios_cover_flow.gif)

```javascript
// 三张图片都放在app.js 同级目录下。
var view = Titanium.UI.iOS.createCoverFlowView({
  backgroundColor:'#000',
  images:['a.png','b.png','c.png']
});
window.add(view);
```
