Welcome to Javascript Function World!

# Function

虽然Javascript支持多种programming style，这其中包括Procedure-Oriented,Object-Oriented, Functional Programming。
但是以我个人（高跃华）来看，Javascript是一个以function为中心的语言，functional programming的成分更多一点。

### Function命名的几个原则
- likeThis()和like_this()二选一(CamelCase和ruby式，二选一 )
- 应该使用动词(verb)加名词(noun)的命名方式,动词在前，print_props()
- 内部(internal)函数或需要隐藏(hidden,或者说不是public API的一部分)，应该使用下划线开头_privateFunction()
- 使用频率非常高的方法，可以牺牲function的可读性，让function name尽量短，比如JQuery框架的$()function

### 一个非常重要的问题（hoisted的问题）
对于刚刚开始写程序的同学来说，会面临一个很重要的问题，*如何组织自己的代码* !
其中一个非常典型的问题就是：*在Javascript当中，function是不是要先定义，才可以调用*。

一句话回答：No!

我相信，写过C或者Ruby同学都会知道，在C程序里面，function只要在main函数开始之前声明一下，就可以在main(主函数)里面调用了，定义往往放在main的后面。
Ruby的很多标注库(standard library)也是这么设计的，method definition会放在调用(call)之前。
在Javascript中，function是hoisted(上移)。

所以，我想你已经知道如何组织自己的代码了。

### Function Declaration Statement

```javascript
// Print the name and value of each property of o. Return undefined.
// 打印object的每一个property的name和value。返回undefined。
function print_props(o){
   for(p in o){
      console.log(p + ": " + o[p] + "\n");
   }
}
```

```javascript
//打印两个点之间的距离。返回浮点数。
function distance(x1, y1, x2, y2){
  var x = x2 - x1;
  var y = y2 - y1;
  return Math.sqrt(x*x + y*y);
  }
```
### Recursive Function
这个例子完全是functional programming的思想。比如在Elixir当中，根本没有类C语言的循环(while,for循环)，循环的地方都使用recursive function。
```javascript
function factorial(x){
  if (x < 1) return 1;
  return x * factorial(x - 1);
}
```
### Function Expression
把function当做数据(data)去处理
```javascript
var square = function(x) { return x * x ;}
```

### 调用function的几种正确姿势
- as functions(当做函数),
- as methods(当做方法),
- as constructors, and
- indirectly through thier call() and apply() method (通过call()和apply()间接调用)

下面依次举例:

As Function
```javascript
print_props({x:1})
var total = distance(0, 0, 2, 1) + distance(2, 1, 3, 5)
var probability = factorial(5) / factorial(13)
```

As Method
```javascript
var calculator = {   // an object literal
  operand1: 1,
  operand2: 2,
  add: function() {
    this.result = this.operand1 + this.operand2;
  }
};

calculator.add(); // 方法调用
calculator.result; // => 3
```
As Constructor

Construtor跟普通function(regular fucntion)或者method，在处理三个东西上的方式是不一样的
- handling of arguments（处理参数）
- invocation context（this代表的是哪一个object）
- return value（返回值）

TODO: apply(), call()
```javascript
var a ;

```
