#coffee(CoffeeScript)
CoffeeScript是一种用来编译成JavaScript的小巧语言。它最简洁的方式展示了JavaScript语言中最优秀的部分。

CoffeeScript会一一对应的解释成JavaScript，在编译的过程中不会进行解释。现已有的JavaScript类库可以无缝的与CoffeeScript结合使用。

##安装
```
sudo npm install -g coffee-script
```

下面我们看看一些CoffeeScript与JavaScript的比较：

`官方网站的CoffeeScript代码`
```javascript
# 赋值:
number   = 42
opposite = true

# 条件:
number = -42 if opposite

# 函数:
square = (x) -> x * x

# 数组:
list = [1, 2, 3, 4, 5]

# 对象:
math =
  root:   Math.sqrt
  square: square
  cube:   (x) -> x * square x

# Splats:
race = (winner, runners...) ->
  print winner, runners

# 存在性:
alert "I knew it!" if elvis?

# 数组 推导(comprehensions):
cubes = (math.cube num for num in list)
```

`对应的JavaScript代码`

```javascript
var cubes, list, math, num, number, opposite, race, square,
  __slice = [].slice;

number = 42;

opposite = true;

if (opposite) {
  number = -42;
}

square = function(x) {
  return x * x;
};

list = [1, 2, 3, 4, 5];

math = {
  root: Math.sqrt,
  square: square,
  cube: function(x) {
    return x * square(x);
  }
};

race = function() {
  var runners, winner;
  winner = arguments[0], runners = 2 <= arguments.length ? __slice.call(arguments, 1) : [];
  return print(winner, runners);
};

if (typeof elvis !== "undefined" && elvis !== null) {
  alert("I knew it!");
}

cubes = (function() {
  var _i, _len, _results;
  _results = [];
  for (_i = 0, _len = list.length; _i < _len; _i++) {
    num = list[_i];
    _results.push(math.cube(num));
  }
  return _results;
})();
```

##用法
从上面的例子可以看出来，CoffeeScript相对JavaScript来说写法极其简洁，可读性也非常强。一般来说，使用CoffeeScript能够减少三分之一的代码量，极大的节约了我们的开发时间。

在CoffeeScript中，使用`->`来表示`function`，方法中的大括号一般也是可以省略的，以及方法的最外层小括号之类的。

##编译方法
coffeescript文件的后缀是`.coffee`，使用`coffee -c` 命令来把coffee文件编译成同名的js文件。


# coffee 语法入门

## 跟ruby一样的地方：
最外层的（） 可以省略
if , unless 可以放在行末
使用缩进。
方法声明，用 ->
for x in [a,b,c]  也可以放在末尾。

## 高级用法
可以声明class , 具备 相应地面向对象功能。 而原生的class就很脆弱，而且很多功能都不具备。
可以 =>
可以在其中 嵌套原生的js


## 目的：
简化编程  ( coffee代码，比原生js， 体积比例： 0.75~ 0.8）省下的，都是 ; , (), [], {}
强化表述力（if, unless, when..then .. )
增强js的能力（class， 继承... ）

大名鼎鼎的nodejs ， 前期用raw js ， 后期就是全都用的coffee写的源代码。


## 用coffee,  必须同时用grunt

写的coffee,可以瞬间被监控到变化，瞬间被编译成 .js 文件。就好像我们写的就是raw js 一样。
