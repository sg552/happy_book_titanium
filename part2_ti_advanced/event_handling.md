# Titanium中的事件处理
主要是针对1.事件处理 2.用户界面事件 3.冒泡和非冒泡事件 4.射击事件 5.自定义事件 6.应用级事件 7.移除事件监听器 8.特殊事件

###1.添加监听事件:

```javascript
 function doSomething(e) {
      Ti.API.info('The '+e.type+' event happened');
      }
      button1.addEventListener('click', doSomething);
      button2.addEventListener('click', doSomething)
```
提示：一个UI元素必须有其touchenabled属性设置为true来触摸相关事件的反应（点击，singletap，等）。在大多数情况下，用户界面组件默认值为真值。然而，如果你发现一个元素不回应事件，尝试设置touchenabled =真的来看看是否有帮助。如果一个观点touchenabled设置为false，触摸事件传递到堆栈中的下一个视图（例如，一个潜在的兄弟姐妹或父母的观点）。

###2.用户界面事件:
 UI事件冒泡的观点，实际上是通过父视图感动（对象继承自Titanium.UI.View），以及某些“视图”对象作为容器的观点。
 例如，一个tableviewsection对象作为一个tableviewrow对象的容器。然而，在iOS的tableviewsection，本身并不是一个视图。因为它是一个逻辑容器，它将在鼓泡链中起作用。从事件的角度看，该节作为其包含的行的父，并且该表作为其行的父。
 一些特殊的容器，如窗口，在视图层次结构中没有父母，所以当它到达一个特定的容器时，事件发生冒泡。这些特殊的容器包括：
 NavigationWindow  SplitWindow  Tab  TabGroup  Window

###3. 冒泡和非冒泡事件
 事件表示用户输入（点击，touchmove，刷卡）是冒泡的事件。其他的事件，如焦点和滚动，都是针对特定的。它们代表了对用户输入的反应，并且它们不起泡。
 下面的事件：
 click
 dblclick
 doubletap
 longclick
 longpress
 pinch
 singletap
 swipe
 touchcancel
 touchend
 touchmove
 touchstart
 twofingertap


###4. 射击事件
 你可以触发事件，而不是等待用户或系统来启动它们。例如，你可以模拟一个按钮按下按钮的点击事件。你会使用类似的代码：

```javascript
someButton.fireEvent('click');

someButton.fireEvent('click', {kitchen: 'sink'});

someButton.addEventListener('click', function(e){
  Ti.APP.info('The value of kitchen is '+e.kitchen);
  });


```

###5.自定义事件
手动设置的点击事件演示了Titanium的事件系统的灵活性，但它可能不是你会做的事情，往往。您可以（和可能会）经常发生fire您自己的自定义事件。例如，当数据库更新时，可能会发生自定义事件。任何依赖于数据库的组件，例如表，可以听该事件和更新自己。这促进了我们的组件之间的松散耦合，使更多的可扩展性和可维护性的JavaScript代码。


```javascript

deleteButton.addEventListener('click', function(e){
        theTable.fireEvent('db_updated');
        });
        theTable.addEventListener('db_updated', function(e){
           theTable.setData(database.getCurrentRecords());
        });
```
###5.应用级事件
应用程序级事件是全球到您的应用程序。他们在所有的情况下，功能范围，CommonJS模块是可访问的，等等。你解雇他们，听他们通过TI应用模块。他们是定制的，在上下文中发送自定义事件。更新以前的代码示例使用应用程序级别的事件让我们这样：

```javascript

deleteButton.addEventListener('click', function(e){
        database.doDelete(e.whichRecord);
        Ti.App.fireEvent('db_updated');
          });
        Ti.App.addEventListener('db_updated', function(e){
            theTable.setData(database.getCurrentRecords());
            someOtherComponent.doSomethingElse();
        });
```
记住，应用程序级别的事件是全局性的，这意味着他们仍然在上下文中的整个应用程序运行（除非你删除它们）。这也意味着，任何对象，他们的参考也将保持在范围内，而你的应用程序运行。这可以防止这些对象被垃圾收集。查看管理内存和查找更多信息的泄漏章节。

###6.移除事件监听器
你可以删除一个事件监听器，从而防止相关组件在将来对事件做出反应。让我们说你有一个删除按钮，只有当一个或多个项目被选中时才是有效的。当用户检查第一项时，可以将单击事件监听器添加到删除按钮。如果用户清除了最后的复选标记，您将从删除按钮中删除事件监听器。
要删除一个事件监听器，您必须传递一个引用到指定的功能，当您添加事件监听器时。换句话说，通过addeventlistener()和removeeventlistener()函数签名必须匹配。最简单的办法是使用命名函数在addeventlistener()声明，所以你也可以通过相同的函数名，删除监听器。

```javascript
  function doSomething(e) {
    // do something
    }
    deleteButton.addEventListener('click', doSomething);
    deleteButton.removeEventListener('click', doSomething);
    });
```
