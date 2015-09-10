Welcom to Best Practices In Titanium!

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

### 代码格式要求
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

TODO:加上示例代码
### function命名
function的命名规范非常重要，function的名字对代码的可读性的影响是非常大，进而影响到整个项目的可维护性。(可读性差的代码，程序员会本能的抗拒)

标准是：
- function的名字一律采用动词(verb)加名词(noun)的方式进行命名
- 具体写法上，必须采用CamelCase的命名方法,即普通方法使用likeThis()命名，constructor使用LikeThis命名


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
