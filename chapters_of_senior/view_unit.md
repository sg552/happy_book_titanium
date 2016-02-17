# 尺寸单位

UI.View 是所有 UI的基础。了解尺寸单位有助于实现不同平台的视图适配。

Titanium中可用的尺寸单位有：

- 纯数字（即不加单位），则是使用的默认单位
- 如果加了单位：
  - 可以是百分比，如: 10%
  - 也可以是：
    - px (pixel)
    - dip (apple的points)
      - 在安卓上一个 DIP相当于 160DPI设备的一个像素
      - 在ios上： 对应一个 非retina设备的一个像素，  对应retina设备的两个像素。
    - in(英尺）
    - mm(毫米）
    - cm（厘米）
    - pt (point),
    该point 是 typographical point, 1 inch的 1/72,
    只在android中可用。在其他系统中，pt仅用于 字体大小。
    不要把它 同苹果的 point弄混)

尽量不要使用 inche, cm, mm， 它跟设备的规格有直接关系，而且容易不精确。

如果没有指定单位，Titanium就会使用该平台默认的单位：

- Android: Pixel
- IOS: DIPS

如果希望对 Android 和 IOS 设置默认的单位，可以在tiapp.xml中使用如下代码：

```xml
<property name="ti.ui.defaultunit" type="string">dip</property>
```

