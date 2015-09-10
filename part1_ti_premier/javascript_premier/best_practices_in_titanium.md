Welcom to Best Practices In Titanium!

# TODO:稍后会出目录结构规范
# TODO: 关于muti-context app如果利用global namespace的问题()
## 因为如果使用CommonJS的pattern的话，每一个module有自己的global namespace，而且没有权限操作app's global space,那么就产生了一个问题：多个页面之间如何共享数据的问题

# TODO:图片处理的规范（理论基础+实践例子）

以下是我对Titanium应用开中的，制定的开发规范(草案)。

编号是RFC 0。

大体上讲，标准主要包括一下几个方面：
- 必须模块化，结构化
- 代码格式要求
- function的命名标准
- 通用的组件必须要封装
- 优化网络请求


具体的内容如下

### 模块化，结构化

开发过程中，必须要讲代码模块化(modular),结构化(structure)。


标准是：
- 每一个页面单独放在一个js文件里面
- 每一个js文件只能暴露一个global variable(使用object或者function作为namespace进行模块化)
- 只在一个js文件使用的function(private function), 必须使用function作为namespace将起private话
- 使用CommonJS进行模块化

### 代码格式要求(一致的代码风格，可以让团队成员的注意力专注于你的代码“说”了什么啊，而不是你是“如何说的”)
- 双操作符的两侧，有且只能有一个空格(a = b；a + b； a == b)
- property name和冒号(:)之间不准有空格，冒号和property value之间，有且只能有一个空格
- 多个变量同时声明的时候，逗号分隔符后面有且只能有一个空格(a, b, c)
- 参数必须要使用圆括号括起来，不能省略(当然，这也是js的硬性规定)
- function name和把参数括起来的圆括号之间不能有空格(function hello(a, b)), 跟后面的花括号有且只有一个空格
- object literal的写法中，property和包裹他们的花括号之间，不能有空格
- 作为参数传递的object，如果property的数量小于三({x: 1, y: 2, z: 3})，则写在同一行，如果大于三，则每一行写一个property。如果object是数组元素，除外。
- 代码的整体结构上，function的使用放在前面，定义同一放在末尾
- global variable的声明上，var不能省略，必须要写！
- 同一使用两个字符的缩进
- 使用双引号，拒绝使用单引号，everywhere
- 尽量避免使用if...else，会拖慢app的performance
- 不能多次使用device-related property,会严重拖慢performance，如果确实多个地方用到了同一个device-related property,那么应该把它赋值给一个变量
- global events handle global objects, 全局的时间，只能处理全局对象，不要跟局部的对象产生关系！比如Ti.App.addEventListener不能绑定局部的UI元素
- 分号不能省略，即使是在optional的地方。所有expression和statement的结尾，必须要有分号，不能省略！
- 变量的命名上，使用category noun开头，比如productTitle, productPrice, productBrand等。
- 对于primitive type object，不要使用constructor！实际的反例就是短信验证码的随机数生成程序，使用了new Array()这样的东西去生成数组（在我们悦家App项目中）
- 常量使用NAME_LIKE_THIS这样的命名方式
- 设计function的时候，要多考虑是否可以使用nested function，鼓励使用nested function
- nested function definiton要使用function definition statement
- 在block里面(比如if条件判断中)，应该使用function definition expression
- 在用到API的时候，有限考虑standard API(ECMA给出的标准API，即ECMAScript标准)，而不是自己写，或者使用第三框框架，比如ES 5支持map()，forEach()等处理数组的function，就不要自己去用其他的
- 删除object的某个属性的时候，应该有限使用null，而不是delete这个operator。比如this.foo = null，而不是delete this.foo
- 对于较长的字符串，比如好几行的那种，必须要使用字符串拼接，而不是使用反斜杠(\)转义
- 起始花括号要跟跟内容在同一行，结尾花括号要单独在一行
- function defintion(函数定义)的时候，arguments(参数)最好写在一行上，如果写不下，就以圆括号为准对其
- 逻辑上一直的代码（比如操纵的是同一个UI组件），必须写在一起，逻辑不同的代码之间，要有一个空行隔开！(所以，你要熟悉你代码的逻辑)
- 必要的情况下，标注variable和function的可见性！在comment里面使用@private, @protected这样的字样
TODO:加上示例代码
### function命名
function的命名规范非常重要，function的名字对代码的可读性的影响是非常大，进而影响到整个项目的可维护性。(可读性差的代码，程序员会本能的抗拒)

标准是：
- function的名字一律采用动词(verb)加名词(noun)的方式进行命名
- 具体写法上，必须采用CamelCase的命名方法,即普通方法使用likeThis()命名，constructor使用LikeThis命名
- verb最好是category verb。比如，getRemoteImages(), getRemoteProducts(), getPersonName(), getPersonAddress()


### 通用的组件进行封装
通用的组件封装，并不是普通意义上的抽取重复代码，封装成一个方法或者function，而是要讲一个完整的功能，比如http请求，封装在一个单独的文件里面，供大家统一使用。

已经封装好的组件，大家必须统一使用，不能自己另外写一套东西，单独用。

通用的组件，大概包括一下几个方面：
- 通用的http请求function
- 通用的缓存文本文件的function
- 通用的缓存图片的function
- 使用本地相册以及调用摄像头的封装

标准是:
- 封装在单独的文件中

### 优化网络请求

这一点要跟后端的接口配合，合理设计接口，将相关数据通过一个接口返回回来。减少访问接口的数量，只能必要的时候访问接口。

标准是：
- 暂定


### 函数式 vs 面向过程

我个人观点，认为js是一门以函数(function)为中心的语言，大家应该使用functional programming的思想去些js代码，不应该把js当成C去写。

脚本语言，虽然都是动态，弱类型，但是各有不同！

比如：
- Javascript程序，应该以function为核心进行设计，把函数(function)当数据。
- Ruby应该以对象为中心进行设计

### code review

项目组的人，每天在下班之前，要开一个小会，由专门人负责，进行code review，做到每个人，对代码的状态有所了解。

具体做法，轮值，每天由一个人牵头，每个人将自己的代码展示给项目组里面的其他人看，说明它代码的设计思路，
要解决的问题，然后大家对他的代码尽心评审。
