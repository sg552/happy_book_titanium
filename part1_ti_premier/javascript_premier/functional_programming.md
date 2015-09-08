Welcome to Functional Programming.

# Functional Programming

### Nested Function Definition(嵌套函数定义)
在Ruby和Javascript当中，function或者method是可以嵌套定义的。

来看Javascript中的例子：
```javascript
// 计算直角三角形(hypotenuse)的面积
function hypotenuse(a, b){
  function square(x) { return x * x ;}
  return Math.sqrt(square(a) + square(y));
}

hypotenuse(3, 4) // => 5.0
```
通过上面的例子，我们可以看到在一个function定义当中，可以定义另一个function。

我们在来看Ruby当中是如何嵌套定义method的。

*注意*:在Ruby，并不存在nested method，写在这更大程度上为了跟js的代码，在形式上进行对比。
```ruby

# 跟上面的js代码功能是一模一样的
def hypotenuse(a, b)
  Kernel.send(:define_method, :square) do |x|
    x * x
  end

  Math.sqrt(square(a) + square(b))
end

# 或者可以像下面这样写
def hypotenuse(a, b)
  def square(x)
    x * x
  end
  Math.sqrt(square(a) + square(b))
end

hypotenuse(3, 4) # => 5.0
```

### Closure
Closure（闭包），闭包是functional programming的一个概念。

Functional programming language是function为中心组织自己的代码，某种程度上跟Procedure-Oriented language非常像，并没有像Object-Oriented language，比如Java，Ruby那样的private关键字，可以私有方法(method)，而Object-Oriented本身就是为了数据封装而设计的，所以自然支持对数据的封装，保证了数据的私有化。

但是私有化，或者说局部化，或者说合理的namespace结构，是所有程序语言必须要具备的能力。

先来看两段简单代码，简单体会一下closure。
```javascript
var scope = "global scope";
function checkscope(){
  var scope = "local scope";
  return scope;
}

checkscope(); // => "local scope"
```

```javascript
var scope = "global scope";
function checkscope(){
  var scope = "local scope";
  return function(){ return scope; };
}

// 重点就在下面这一行，理解为什么返回的是下面的值，就算是closure入门了。
checkscope()(); // "local scope"
```

下面这段代码，解释了闭包的实际作用。即，使用function作为一个隔离层，跟global scope隔离开，避免跟global scope冲突，或者说污染global scope。

```javascript
var counter = (function() {
  num = 0;
  return function() { return ++num; };
}());
counter(); // => 1
counter(); // => 2
```
最后使用Javascript代码和Ruby代码对比的方式，说明对于closure这个概念，普通的语言是如何实现的。

Javascript代码：
```javascript
function counter(){
var n = 0;
return {count: function(){ return ++n; },
        reset: function(){ n = 0; }
       };
}

var c = counter(), d = counter();
c.count(); // => 1
d.count(); // => 1

c.count(); // => 2
d.count(); // => 2

c.reset(); // undefined
c.count(); // => 1
d.count(); // 3
```

Ruby代码：
```ruby
class Counter
def counter
n = 0
Kernel.send(:define_method, :count) do
n += 1
end

Kernel.send(:define_method, :reset) do
n = 0
end
end
end

c = Counter.new; c.counter
d = Counter.new
c.counter # => 1
d.counter # => 2

c.counter # => 3
d.counter # => 4

c.reset # => 0
c.counter # => 1
d.counter # => 2
```
希望读者可以通过以上简单的小例子，对closure概念有一个了解。

因为我们知道很多语言的编译器都是使用Ｃ语言编写，比如说Ruby等。

Ruby的语法本身，只是封装了一套Ｃ API。所以，从这个角度讲，了解C是如何处理变量scope，就很有必要了。

C通过三个维度对变量进行描述，分别是：
- 存储时期(storage duration)
- 作用域(scope)
- 链接(linkage)

存储时期有两种：
- 静态存储时期(static storage duratoin)
- 自动存储时期(automatic storage duration)
链接类型分为三种：
- 外部链接(external linkage)
- 内部链接(internal linkage)
- 空链接(no linkage)

根据这三个维度的组合，C为变量定义了五种存储类型(其实，还有一种基于指针的类型)。

这五种存储类型分别为：
- 自动(auto)
- 寄存器(register)
- 具有代码块作用域的静态
- 具有外部链接的静态
- 具有内部链接的静态

以下将通过简单的C代码，来说明在C中是如何表达这五中存储模型的。
