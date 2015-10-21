# Underscore

TODO:
整篇文章冗长,代码也没标示出来,与http://www.css88.com/doc/underscore/这篇文章大部分类似。

> refer to:  http://docs.appcelerator.com/backbone/0.9.2/#Collection-Underscore-Methods

**backbone**中的**underscore**提供了28个操作集合的方法.  用好它们可以极大的提高我们的工作效率.

##简介
   underscore是一个javascript的实用库，为我们提供了一系列的强大的函数式编程的工具，帮助我们更为快速便捷的开发web程序。

##安装
Node.js 下安装:

```
npm install underscore
```

##underscore下的collections

> 本文中 `=>` 表示输出内容

这小节主要介绍underscore下的一些常用的collections

each: `_.each(list, iteratee, [context])  alias:foreach`

each 函数用来遍历操作list中的每一个元素，当我们传递一个context参数时，list 中的每个元素会被迭代的绑定context操作，顺序执行。如果list是一个javascript对象，迭代的参数将会时（value，key，list），返回一个list对象
以便于链式操作。

需要注意的是：collection functions可以正常应用在数组（arrays），对象（objects）以及一些类似的数组对象例如arguments，Nodelist等，但是其是基于鸭子模型（duck－typing）工作的，所以我们应该尽量避免传递不确定长度的
参数给该类方法。同时我们应该注意到每个each循环不能够用break来打断，应该使用_.find来作为替代。

map: `_.map(list,iteratee, [context])   alias:collect`

map 函数使用转换函数（iteratee）通过遍历list中的每一个值产生一个新的数组。转换函数（iteratee）传递三个参数：值（value），迭代index（或者key），以及一个指向新生成的数组对象(list)的引用。

```javascript
_.map([3,4,5],function(num){return num * 5; });
=> [15,20,25]
```

reduce: `_.reduce(list, iteratee, [memo], [context])  alias:inject, foldl
`

reduce函数又被称为inject和foldl，该函数方法把list中的每一个值转换为一个单独的值（value）。memo是reduction（reduce函数）的初始状态，后面的每一步操作都应该是通过迭代器（iteratee）返回。迭代器（iteratee）传递四个参数：
memo，迭代器的value（或者key）和index，指向整个list的引用。

如果我们没有给reduce传递初始的memo，那么迭代器在初次调用时将会使用list的第一个元素作为初始的memo，然后从下一个元素开始迭代操作。

```javascript
_.reduce([1,2,3], function(memo, num){return memo * num];}, 1)
=> 6
_.reduce([1,2,3], function(memo, num){return memo * num];})
=> 6
```

reduceRight:`_.reduceRight(list, iteratee, memo, [context]) alias:foldr`

和上一个reduce函数类似，reduceRight 是从最右侧开始操作list中的每个元素。

```javascript
var list = [ [0,1],[2,3],[4,5]];
var flat = _.reduceRight(list, function(a, b) { return a.concat(b); }, []);
=>[5,4,3,2,1,0]
var flat2  = _.reduce(list, function(a, b) { return a.concat(b); }, []);
=>[0,1,2,3,4,5]
```

find:  `_.find(list, predicate, [context])   alias: detect`

find函数通过逐项查找list中的每一个元素，返回第一个通过迭代函数（predicate）检测正确的值，如果没有找到通过检测的数值则会返回undefined,find函数并不会每次都遍历list中的每个元素，当其匹配到通过检测的值时就会返回，而不是继续检测完整个
list。

```javascript
var event = _.find([1,2,3,4,5,6], function(num){return num%3==0;});
=> 3
```

filter:  `_.filter(list,predicate,[context])  Alias:select`

fliter函数遍历list查找出符合检测函数（predicate）的元素。

```javascript
var event = _.find([1,2,3,4,5,6], function(num){return num%3==0;});
=>[3,6]
```

where:  `_.where(list,properties)`

where函数遍历list，返回一个包含properties所列出属性的所有键值对的数值。

findWhere:  `_findWhere(list,properties)`

与where函数类似，只是findWhere函数返回的是第一个匹配到的包含properties所列出属性的键值对的数值。同时需要注意的是如果没有匹配到相应的属性，或者list为空时，会返回undefined。

reject  _reject(list,predicate, [context])

reject函数与filter函数相反，该函数通过遍历list中的每一个元素，返回所有不符合检测函数（predicate）检测的元素。

```javascript
var event = _.find([1,2,3,4,5,6], function(num){return num%3==0;});
=>[1,2,4,5]
```

every: `_.every(list,[predicate], [context])  Alias:all`

如果list中的每一个元素都通过检测函数（predicate）的检测，就返回true，否则返回false。

some:  `_.some(list,[predicate],[context])   Alias:any`

如果list中有某一个元素通过了检测函数（predicate）的检测，就返回true，否则返回false。

contains: `_.contains(list, value, [fromIndex])  Alias:include`

如果list包含指定的value就返回true。如果是list数组（arrays），那么内部使用indexOf判断，使用fromIndex来确定开始的起始位置。

invoke: `_invoke(list, methodName, *arguments）`

在每一个list元素上执行methodName的函数方法，任何传递给invoke的额外参数，invoke都会在调用methodName方法的时候传递给它。

```javascript
_.invoke([[5,1,7],[3,1,2]],  'sort')
=>[[1,5,7],[1,2,3]]
```

还有pluck，max， min等等。有兴趣的同学可以查阅相关的文档

> 官方文档<http://underscorejs.org/>

> 参考文档<http://javascript.ruanyifeng.com/library/underscore.html>

##underscore下的ArrayFunctions

> 注意：所有的array functions都可以在arguments object上正常使用，但是undersocore functions并不是只针对稀疏数组（sparse arrays）设计的。

first: `_.first(array, [n])   Alias:head,take`

initial:  _.initial(array,[n])   

last    _.last(array, [n])    rest   _.rest(array,[n])   Alias:tail,drop

上面几个函数的功能比较相似，所以统一介绍一下，first函数返回数组（array）的第一个元素，传递的参数n代表返回前n个元素。initial函数返回除最后一个元素之外的所有元素的数组，该函数在
arguments object的使用上特别有用，传递的参数n表示排除后面的n个元素。 last函数返回最后一个元素，传递的参数n代表返回最后面的n个元素。 rest函数返回除第一个元素之外的其他元素，传递
的参数index表示返回从该数值之后的所有元素。

```javascript
var list = [5,4,3,2,1];
_.first(list, 2);
=>[5,4]
_.initial(list);
=>[5,4,3,2]
_.last(list,2);
=>[2,1]
_.rest(list,3);
=>[2,1]
```

compact  _.compact(array)

返回一个除去所有falsy值的array副本，在javascript中，false，null，0，"",undefined和NaN都是falsy。

```javascript
_.compact([0,1,false,"",null,NaN,2]);
=> [1,2]
```

flatten  _.flatten(array,[shallow])

将一个多层嵌套的数值array（嵌套可以是任意层的）转换为只有一层的数组，但是当shallow传参为true时，数组只会转化第一层。

```javascript
_.flatten([1,[2],3,[[[4]]]]);
=>[1,2,3,4]
_.flatten([1,[2],3,[[[4]]]],true);
=>[1,2,3,[4]]]
```

without  _.without(array,[*values])

返回一个除去所有的values之外的array副本。

```javascript
_.without([1,2,3,4,1,2,4,],1,2);
=>[3,4,4]
```

union   _.union(*arrays)

返回传入的数组（arrays）的并集：按顺序返回，返回的数组的元素是唯一的，可以传入一个或者多个数组（arrays）。

intersection  _.intersection(*arrays)

返回传入数组（arrays）的交集。

difference   _.difference(array, *others)

和without函数类似，但是返回的值来源与在其他数组（arrays）中不存在的值。

```javascript
_.difference([1,2,3,4,5],[1,2,3]);
=>[4,5]
```

unip  _.unip(array, [isSorted], [iterator])   alias:unique

返回array去重后的副本，使用===操作符做相等测试。当我们传值true给isSorted时，表明我们对于array已经进行排序，这时unip函数将会采用更快的算法
，如果要处理对象元素，传参iterator来获取需要比对的属性。

zip   _.zip(*arrays)

合并arrays里每一个数组的每一个相对位置的元素，并保留在相对应的位置上，这个函数在合并分开保存的数据时很有用。如果你要合并矩阵嵌套数组的话，
_. zip.apply能够变换矩阵达到类似的效果。

```javascript
_.zip(['lisi','zhangsan','sunmei'],[30,20,28],['man','man','woman']);
=>[ [ 'lisi', 30, 'man' ],
  [ 'zhangsan', 20, 'man' ],
  [ 'sunmei', 28, 'women' ] ]
```
unzip   _.unzip(*arrays)

和zip函数的功能恰好相反，把给定的arrays，分解为一串相应的新数组。其中第一个数组存放的是输入数组的第一元素，第二个数组存放的是输入数组的第二元素，
以此类推。

```javascript
_.unzip([['lisi',30,'man'],['zhangsan',20,'man'],['sunmei',30,'woman']]);
=> ['lisi','zhangsan','sunmei'],[30,20,30],['man','man','woman']
```


函数（functions）

bind   _bind(function,object,*arguments)

绑定函数（function）到对象（object）上，意味着无论何时我们调用函数，this的值都是指向object对象的。可选参数arguments可以传递给函数function，可以填充
函数所需要的参数，这也被称为partial application 。对于meiyou结合上下文的partial application绑定，可以使用partial

```javascript
var func = function(greeting){return greeting + ":" + this.name};
func = _.bind(func, {name: 'lisi'}, 'hi');
func();
=>'hi:lisi'
```

bindAll   _bindAll(object, *methodNames)

个人认为是bind方法的升级版，绑定methodNames指定的方法到对象odject上，当这些方法被执行时调用这些方法就会在对象的上下文环境中执行，绑定函数用作事件处理
函数时十分方便，否则函数调用时this一点用处都没有，methodNames参数是必须的。

partial   _.partial(function, *arguments)

局部应用一个函数填充任意数目的arguments，不改变其动态的this值。和bind方法很类似。同时你也可以传递一个_在你传递的arguments列表中间指定一个不预先填充
只在调用时动态提供的参数。

```javascript
var sub = function(a,b){return a+b;};
sub5 = _.partial(sub,20);
sub5(20);
=>25
subFrom5 = _.partial(sub,_,20);
subFrom(20);
=>45
```

memoize   _.memoize(function, [hashfunction])

memoize 可以用来缓存某些函数的结算结果。这对于那些需要较长计算时间的函数有较大的帮助作用。如果传递了一个可选的hashFunction，它将会使用hashFunction计算的
返回值作为key来存储计算结果。默认情况下，hashFunction使用function第一个参数作为key来缓存，memoize的值的缓存可以作为返回函数的cache属性。

```javascript
var fibonacci = _.memoize(function(n){
return n <  2 ? n : fibonacci(n -1) + fibonacci(n-2);
});
```
delay  _.delay(function, wait, *arguments)

和setTimeout十分类似，引用function等待（wait）一定的毫秒后，如果你传递了可选的arguments，他们将会在function执行时，被传递给function。

###objects Functions

keys  _.keys(object)

检索object所拥有的所有可枚举的属性的名称

allkeys  _.allKeys(object)

检索object拥有的和继承的所有属性的名称

values   _values(object)

返回object对象所有的属性值

mapObject  _.mapObject(object,iteratee,[context])

类似于map，只不过该方法使用来转换对象的每个属性的值。

```javascript
_.mapObject({first:1, last:5}, function(val,key){
  return val + 4;
});
=>{first:5,last:9}
```

pairs _.pairs(object)

将一个object对象转换成为键值对[key,value]的形式。

```javascript
_.pairs({one:1,two:2,three:3}
=>[['one',1],['two',2],['three',3]]
```

invert  _.invert(object)

返回一个object的副本，把object中键和值互相调换。需要注意的是：在这个操作中必须保证object中所有的值唯一并且可以序列化。

create  _.create(prototype,props)

一句给定的原型创建一个新的object对象，可选附加的props作为own的属性。基本上，和Object.create相同，但是没有所有的属性描述符。

functions   _.functions(object)   Alias:methods

返回一个对象里所有的方法名并且方法名已经经过排序－也就是说对象里每个方法（属性值是一个函数）的名称。

extend   _.extend(destination, *sources)

复制source对象的所有属性到destination对象上，然后返回destination对象，复制是按顺序的，所以后面的对象会把前面的对象覆盖掉（当有
重复时）

```javascript
_.extend({name:'name'},{age:30});
=>{name: 'name',age:30}
```

has _.has(object,key)

对象是否包含给定的键值？等同于object.hasOwnProperty(key),但是使用了一个hasOwnProperty的一个安全引用，以防万一意外重写。

```javascript
_.has({a:1,b:3,c:4},"b");
=>true
```

###Utility

noConflict   _.noconflict()

放弃"_"变量的控制权，并把其交还给其原来的所有者，但会一个underscore对象的引用。

indentity   _.identity(value)

返回和传入参数相等的数值，相当于数学中的f（x） ＝ x
这个看似无用的函数，在underscore中作为默认的迭代器iterator。

constant    _.constant(value)

创建一个返回相同值的函数，这个返回值用来作为 _.constant的参数。

noop  _.noop()

无论传递什么参数，该函数返回的都是undefined。可以用来作为默认的回调参数。

iteratee   _.iteratee(value, [context])

一个重要的内部函数，可以应用到集合的每一个元素中，返回任何想要的结果－无论是等式，任意回调，属性匹配还是内部访问。
使用_.iteratee转换判断的underscore方法的完整列表时map，find，filter，reject，every，some，max，min，sortBy，countBy，
sortedIndex，partition，以及unique。

uniqueId   _.uniqueId([prefix])

为需要的客户端或者dom元素生成一个全局唯一的id，如果传递了prefix参数，那么id将会附加在其上。

now  _.now()

一个优化的获得当前时间的整数的时间戳，可用于实现动画／定时等功能

```javascript
_.now();
=>1444387537273
```

###链式语法

链式语法的主要优点是在js代码中是非常常见的一种语法结构，利用链式语法可以大大简化我们的代码结构，精简代码的书写量，以及提高我们的
编码效率。

当一个对象调用chain方法时，会将这个对象封装起来并让每次方法的调用结束时返回这个对象的封装。当我们完成最终的计算时，可以使用value方法
来取得最终的值。

chain  _.chain(obj)

返回一个封装的对象。调用这个封装对象的方法也会继续返回封装的对象，直到value方法的调用。

```javascript
var s= [{name: 'lal', age:26},{name: 'ha',age :29},{name: 'heu',age:32}];
var ys = _und
         .chain(s)
         .sortBy(function(s){return s.age})
         .map(function(s){return s.name + ' is ' + s.age;})
         .first()
         .value();
=> 'lal is 26'
```

value   _(obj).value()

获取封装对象的最终值

```javascript
_([1,2,3]).value();
=>[1,2,3]
```
