Welcomet to Ti Module World!

TODO: module

写module的注意事项：

## 如何动态的创建View组件

```xml
    <com.amap.api.maps.MapView
        xmlns:android="http://schemas.android.com/apk/res/android"
        android:id="@+id/map"
        android:layout_width="match_parent"
        android:layout_height="match_parent" >
    </com.amap.api.maps.MapView>
```
```java
  // Activity 中。。。
  MapView map_view = (MapView) findViewById(R.id.map);
```


我们则可以在 ViewProxy中(注意动态定义里面的 map_view)：

```java
   public ExampleView(TiViewProxy proxy) {
          super(proxy);

      //layoutParams for holder view
      LayoutParams lp = new LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.WRAP_CONTENT);
      //holder view
      LinearLayout holder = new LinearLayout(proxy.getActivity());
      holder.setLayoutParams(lp);

      map_view = new MapView(proxy.getActivity());
      text = new TextView(proxy.getActivity());

      holder.addView(map_view);
      holder.addView(text);

      setNativeView(holder);

    }
```

## Android中的Bundle

```java
// Activity 中：
    protected void onCreate(Bundle savedInstanceState) {
        mapView = (MapView)findViewById(R.id.map);
        mapView.onCreate(savedInstanceState);
        if(aMap == null) {
            aMap = mapView.getMap();
        }
    }
```

那么，在android module中，则可以：

```java
// ExampleProxy中，定义这个方法, 注意其中的第二个参数，就是Bundle
  @Override
  public void onCreate(Activity activity, Bundle savedInstanceState) {
    map_view.onCreate(savedInstanceState);
    Log.i(LCAT, "====== after map_view.onCreate");
  }
```

## 生命周期
Android Activity 中的 onCreate/Start/Resume... 都可以在 Titanium ViewProxy
中找到对应的方法
这些  onCreate 等方法，写在module中也行，写在proxy中也行

##
