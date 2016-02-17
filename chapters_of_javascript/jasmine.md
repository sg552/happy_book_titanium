# Jasmine : js 测试框架

跟Rspec一样，Jasmine是javascript中的BDD框架。你可以就认为它是一个测试框架。

截止到2015年9月15日，最新的版本是2.3.4。

## 在web浏览器上使用

这是最简单的方式。首先下载zip文件：

```bash
$ wget https://github.com/jasmine/jasmine/releases/download/v2.3.4/jasmine-standalone-2.3.4.zip
```

下载后，直接解压缩, 可以看到该目录结构如下

```bash
▾ lib/                  #  jasmine的核心文件, 不要动。
  ▸ jasmine-2.3.4/
▾ spec/                 # 放置测试的目录
    PlayerSpec.js       # 测试文件
    SpecHelper.js       # 辅助文件，可以增加spec方法等。
▾ src/                  # 源代码 文件夹
    Player.js
    Song.js
  SpecRunner.html       # 看结果的页面
```

因为需要运行在浏览器中，所以我们每次运行测试时，直接打开 `SpecRunner.html` 这个文件。

![jasmine SpecRunner 运行结果](/images/jasmine_default.jpg)

## 在node中使用

```bash
$ npm install jasmine-node -g
```

运行方式：

```bash
$ jasmine-node spec/
```

jasmine-node 也可以直接运行coffeescript:

```bash
$ jasmine-node --coffee spec/AsyncSpec.coffee spec/CoffeeSpec.coffee spec/SampleSpec.js
```

## 一些matcher例子

expect, toBe, toEqual, not 等等。

```javascript
describe("Included matchers:", function() {

  it("The 'toBe' matcher compares with ===", function() {
    var a = 12;
    var b = a;

    expect(a).toBe(b);
    expect(a).not.toBe(null);
  });
});
```

## 使用 describe 来对 it进行分组

## setup 和 teardown

有beforeEach, beforeAll, afterEach, afterAll

```javascript
  beforeEach(function() {
    foo += 1;
  });

  afterEach(function() {
    foo = 0;
  });
```

##  pending

```
  pending('this is why it is pending');
```
