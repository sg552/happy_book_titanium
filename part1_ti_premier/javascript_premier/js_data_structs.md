Javascript中的基本对象是Object，还有就是数组(Array)。

对象(object):
```Javascript
{x: 1, y: 1}
```

数组(array):

```Javascript
[1, 2, 3]
```

因为前面一定提到了Object，所以这里我们仅仅介绍数组（Array）的使用方法。

从数组里拿数据:

```Javascript
var arr = [1, 2, 3];
arr[0] // 1
arr[1] // 2
```

往数组里面加数据:
```Javascript
arr[2] = "Hello, world"
```
以下是访问我们首页轮播图的接口，返回的json数据(接口地址是testcms.yuehouse.co/interface/init/home_sliders)

这是我们在日常开发中特别典型的json
```javascript
{
success: true,
result: {
home_sliders: [
    ["/uploads/home_scroll_image/image/31/indexlink0727.jpg", "order_form"],
    ["/uploads/home_scroll_image/image/32/2.jpg", "stand_packages"],
    ["/uploads/home_scroll_image/image/34/4.jpg", "finance"]
]
       }
}
```
- success对应一个bool值，即true
- result对应一个object，即home_sliders:数组
- home_sliders对应一个数组，这个数组里面包含三个数组

这其中，有三个property：success, result, home_sliders

| property name | property value |
|---------------|----------------|
| success       | true           |
| result        | object         |
| home_sliders  | [array1, array2, array3]|


TODO
### 可以写一些数据结构的问题，也就是如何选择更加合理的数据结构去表示我们的数据，最好结合实际的例子，进行对比的写。
