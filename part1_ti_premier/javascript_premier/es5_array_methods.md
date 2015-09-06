ES 5中对Array新增加了5个新的支持函数式编程的方法。

### forEach()
```javascript
var data = [1,2,3,4,5];
var sum = 0;
// value即为数组的元素的值
data.forEach(function(value){ sum += value; }) // 返回值是undefined
sum // sum => 15
//另一种写法,v是数组元素的值，i是数组元素的index，a是数组本身
data.forEach(function(v,i,a)){ a[i] = v + 1; })
data // => [2,3,4,5,6]
```
### map()
```javascript
//map()跟前面提到的forEach()非常像，区别在于map()的返回值是新的数组，而不是forEach()的undefined
a = [1,2,3]
b =  a.map(function(x){ return x * x; }) // b is [1,4,9]
```
### filter()
```javacript
//用于筛选数组中的元素
a = [5,4,3,2,1]
small_values = a.filter(function(x){ return x < 3; }) // [2,1]
odd_values = a.filter(function(x){ return x % 2 == 0; }) // [5,3,1]

//去掉数组中的空元素
var data = [1,,3,4]
data.filter(function(x){ return true; }) // [1,3,4]
// 进一步，去掉数组中的gap，null和undefined
a = a.filter(function(x){ return x != undefined && x != null; })
```
### every()和some()
```javascript
var a = [1,2,3,4,5]
a.every(function(x){ return x > 0; }) // true
a.every(function(x){ return x > 1; }) // false
a.some(function(x){ return x > 3; }) // true
```
TODO: 写完reduce()和reduceRight()

### reduce()和reduceRight()

注：ES的全称为ECMAScript的简称。ES是ECMA(European Computer Manufacturer's Association)关于Javascript的标准。


### 实际开发中的例子
我们在实际的工作环境中，是如何使用以上方法简化我们的代码的。

这是我们之前提到的，请求一个接口返回的json数据。
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

下面是我们如何在悦家手机App中如何处理这些数据的(使用了Alloy框架),为了突出重点，对代码进行了适当的删减。

```coffee
get_home_sliders_process = ->
    remote_data = JSON.parse(this.responseText)
    if remote_data.success
            # 重点在于这里的map()的使用
            remote_data.result.home_sliders.map((url_and_description) ->

            # 将数组中的url和descrip数据分别处理
            image_url = url_and_description[0]
            image_description = url_and_description[1]

            #创建轮播图($.sliders是一个scrollview的id)
            home_scroll_image_view = Ti.UI.createImageView({width:"100%", height:"100%"})
            $.sliders.addView(home_scroll_image_view)

       scroll_dot_view = PagingControl($.sliders)
       $.home_sliders.add(scroll_dot_view)
    else
      console.info("没有轮播图")
```
