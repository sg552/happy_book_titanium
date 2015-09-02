从语言设计的角度看，Javascript是一门设计相对简单的语言，它基于原型的继承模型非常容易理解和上手，对于新手来说非常友好。

Javascript中，对象分为三类：
- ES标准定义的Object，例如Date。
- 宿主环境(host environment)定义的Object，例如浏览器定义的Element。
- 自定义(self defined)定义的Object，也就是自己定义的。

每一个Object有三个属性(object attribute):
- 原型(prototype), Javascript用来实现继承的东西
- 类(class), 说明Object的类型(type)
- 扩展(extensible), 说明Object是否可以被扩展，即是否可以增加或删除Object里面的property

每一个property有也有三个属性(property attribute):
- 可写属性(writable attribute)，说明该property value是否可以被复制。
- 可枚举属性(enumerable attribute), 说明该property本身是否可以被遍历
- 可配置属性(configurable attribute), 说明property value是否可以被删除(delete)或改变(alter)

以下是Javascript中Object的literal写法:
```
var obj = {x:1, y:2}
```

以逗号分隔开的每一个元素，被叫做一个property，比如x:1, y:2是obj的两个property。

以冒号分隔，冒号前面的叫做property name, 比如x, y都是property name；冒号后面的叫做property value，比如1，2。

取值方法:
```
obj.x    // => 1
obj[x]   // => 1
```

赋值方法:
```
obj.x = 2 // x等于2
obj[x] = 2
```
