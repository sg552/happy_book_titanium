#Ti.UI.ListView

##ListView简介

**ListView**是Titanium-UI组件中比较重要的一个UI组件，因其能灵活处理复杂的逻辑数据的绑定和更新，使其
成为UI组件中在处理大型的复杂的逻辑数据时最佳的UI组件选择项；但与此同时它也成为Titanium-UI组件中
最为复杂的UI组件之一。如果你还从没接触过ListView，那么先看看下面的UI效果吧！

![imageview](http://image.happysoft.cc)

从上面的效果图中我们可以看出ListView其实就是一个数据的“**清单list**”UI组件，清单里的每条数据占据清单里
的一行；并且当数据项超过屏幕长度时能自动滚动，每条数据都有其各自的特性(效果图中点击每条数据弹出
的对话框内容可以看出)。下面是实现效果展示图的代码：

_my_list_view.xml:_

```xml
    <Alloy>
        <Window>
            <ListView id='my_list_view'>
                <HeaderView>
                    <View class='header_footer_view_style'>
                        <Label class='header_footer_label_style'>Header View</Label>
                    </View>
                </HeaderView>

                <ListSection>
                    <ListItem>
                        <Label class='list_item_label_style' text='data 1'/>
                    </ListItem>

                    <ListItem>
                        <Label class='list_item_label_style' text='data 2'/>
                    </ListItem>

                        <!--此处省略data 3~data 8-->

                    <ListItem>
                        <Label class='list_item_label_style' text='data 9'/>
                    </ListItem>

                    <ListItem>
                        <Label class='list_item_label_style' text='data 10'/>
                    </ListItem>
                </ListSection>

                <FooterView>
                    <View class='header_footer_view_style'>
                        <Label class='header_footer_label_style'>Footer View</Label>
                    </View>
                </FooterView>
            </ListView>
        </Window>
    </Alloy>
```
_my_list_view.tss:_

```tss
   '#my_list_view':{
      top:'0',
      width:'100%',
      height:'100%',
      backgroundColor:'red'
   }

   '.list_item_label_style':{
      font:{
        fontSize:'12'
      },

      width:'100%',
      height:'100%',
      color:'black',
      textAlign:'left',
      verticalAlign:'center'
   }

   '.header_footer_view_style':{
      width:'100%',
      height:'5%',
      backgroundColor:'purple'
   }

   '.header_footer_label_style':{
      font:{
        fontSize:'15',
        fontWeight:'bold'
      },

      width:'100%',
      height:'100%',
      textAlign:'center',
      verticalAlign:'center'
   }
```
_my_list_view.js:_

```js
   $.my_list_view.addEventListener('itemclick',function(e){
      alert('数据排列序号：'+e.itemIndex+'，'+'数据：'+e.source.text);
   });
```

从**my_list_view.xml**文件中，我们可以大致的看出ListView总共由三部分组成：**HeaderView**、**ListSection**以及**FooterView**。
HeaderView是ListView的**head**头部控件，可以在这里定义头部的样式；ListSection是
LisiView的**body**身体部分，数据都展示在这里；FooterView是ListView的**foot**，定义尾部样式。一般情况
下，除非需要用到HeaderView与FooterView，否则ListView的头部、尾部样式可以不定义，不影响整个UI效
果。除此之外，ListView还可以在顶部(**HeaderView上方**)嵌套一个**搜索栏**，用于对数据的筛选显示。不过，
对于Android与IOS分别有不同的UI组件：

* **SearchBar**，适用于**IOS**；
* **SearchView**，适用于**Android**；(注意在定义时，如果属于静态定义[_**.xml**_文件]则需要声
     明**ns='Ti.UI.Android'**、**platform='android'**；如果属于动态定义[_**.js**_文件]则需要使用**Titanium.UI.Android.createSearchView**方法)


    PS：如果你观察仔细的话，在浏览效果图时你应该会发现ListView中最后一条数据data 10是展示不完全的，ListView滑到底部
        松开后data 10会被屏幕遮挡一部分。这是ListView的一个小瑕疵，正是因为这个小瑕疵，所以当我们的数据size很大，超过屏
        幕长度时我们建议为ListView定义一个FooterView来解决这个问题。此时你可以只需要给这个FooterView定义一个空的任何UI
        组件就行了，它的作用只是为了占据一定的空间来保证我们数据展示的完整性，并没有实际意义。

我们上面介绍的是ListView的静态定义方法，其实更多的时候ListView都是动态定义出来的。因为数据更新的
需要我们无法明确数据的量度，因此需要在_**.js**_中根据远程获取的参数来动态定义，而这就需要绑定数据了。下
面我们将重点详细介绍ListView数据绑定时几个重要的属性及方法。

##ListView数据绑定

###1. ListSection

**ListSection**是ListView的核心部分，处理数据的绑定和渲染等。在ListView中，ListSection区分不同的**数据块**
(**section**本身就有**区域**的意思)，定义了多少个ListSection就有多少个数据块；需要往哪个数据块渲染数据，
则指定该ListSection的**id**进行渲染即可。

####1.1 Sections
**sections**是ListView的ListSection的集合，通过**getSections()**方法获取，返回数组型数据集合。该属性最重要的用法
不在获取ListView的sections的数据集合上，而是在动态创建时用来渲染ListView的ListSection的数据，即**setSections()**方法的使用。

我们已经知道getSections()方法返回的是sections数组型集合数据，那么setSections()方法就是绑定一个数组型的集合数据了。因此我们
可以通过创建一个关于ListSection的多条数据的数组集合来渲染ListView的多个ListSection。下面是参考代码：

```js
   var my_list_sections_data = [
      {properties:{headerTitle:'Data Section 1'}}, //headerTitle是ListSection的一个属性porperty
      {properties:{headerTitle:'Data Section 2'}}
   ]

   $.my_list_view.setSections(my_list_sections_data);

   var my_list_view_sections_length = $.my_list_view.getSections();
   console.info(my_list_view_sections_length) //输出结果为2
```

####1.2 sectionIndex
**sectionIndex**描述ListView中每个ListSection的序号**index**，从0开始。该属性的获取的方法一般不能直接获
取，而需要通过事件参数**e**来获得(关于事件参数e，请参考**第x章**)。我们通过sectionIndex来确定ListView中某个确定的ListSection，进而
能够获取到该ListSection中具体的某一个ListItem的数据。具体代码参考如下：

```js
   //假设我们要获取某个ListSection中的某个ListItem中绑定数据(绑定的id为bind_color，设置为red)的label的颜色属性

   $.my_list_view.addEventListener('itemclick',function(e){
      var label_color = $.my_list_view.sections[e.sectionIndedx].items[e.itemIndex].bind_color.color;
      console.info(label_color); //输出结果为red
   });

   /*itemclick为ListView的点击监听事件，点击某个listItem并通过事件参数e我们可以获取到该ListItem所在的ListSection(e.sectionIndex)，以及
     是该ListSection中哪一个ListItem(e.itemIndex)；再通过绑定的id获取该label的颜色属性。*/
```

通过上面的代码，我们现在能进一步获取ListView中的数据了。关于ListItem、items、itemIndex的使用，我们下面将详细介绍。

###2. ListItem

**ListItem**是ListView的**数据单元**，在ListView中一行即是一个ListItem；但这并不意味着ListItem中所包含的
就是最小的数据单元，因为一个ListItem中可能包含多条数据。(这需要通过**数据模板Template**来实现，不同的
数据模板数据单元的划分也不同)但是进行数据渲染时，最小的渲染数据单元就是ListItem；并且ListView的点击监听事件
也是加在ListItem上，当然你也可以为ListItem中的某个特定的数据设置特有的点击事件，两者并不冲突。

####2.1 Items
**items**是ListSection中所有ListItem的集合，类似sections。获取方法以及设置方法也于sections类似，**getItems()**获取某ListSection中所有ListItem的集合，
返回数组型数据；**setItems()**则为某个ListSection绑定一个数组型的ListItem数据。

```js
   var my_list_items_data = [
      {properties:{title:'item1 data'}}, //title为ListItem设置“标题”
      {properties:{title:'item2 data'}}
   ]

   $.my_list_section.setItems(my_list_items_data);

   var my_list_section_items_length = $.my_list_section.getItems();
   console.info(my_list_section_items_length) //输出结果为2
```

####2.2 itemIndex
**itemIndex**描述ListSection中每个LisetItem的序号index，从0开始，和sectionIndex类似。同样可以通过事
件参数e来获取，参考sectionIndex。

通过上面的介绍我们已经大致了解了ListView获取数据的方法，要获取ListItem中的某个数据，我们要知道该数据在ListSection
中的位置；知道ListItem的位置之后，我们还要获取该ListSection在LisView中的位置；只有这样我们才能精确获取该数据的
具体位置。事实上，在开发中我们很少去动态创建ListSection；即一个页面的数据块的分类一般情况下是已经确定的，即使在不确定
的情况下我们只要在逻辑代码中考虑一下该ListSection没有数据的情况。(如果该ListSection有样式需求，如有headerTitile标题，没有
数据的情况下是不能显示该标题的[或者其他的特殊处理]；那么我们就必须得动态定义该ListSection了)其实，真正需要慎重考虑的是我们对
ListItem中数据的处理；即我们是否能设计一个比较好的数据模板Template来处理比较复杂的数据需求；接下来我们重点介绍数据模板Template。

###3. 数据模板Template
**Template**数据模板描述的是ListView在渲染数据时，数据渲染所要遵循的“**渲染样式**”，即数据在LisView中的结构样式，说白了就是设定好
所要的UI样式，然后将数据绑定到相关的UI组件上。数据渲染主要通过**bindId**来实现，即绑定**id**的UI组件；该组件即用来渲染其对应的数据。
在ListView中，我们可以通过定义**Template**标签来实现；我们所定义的数据样式，其实就是对ListItem中所要填充的数据进行样式定义，即item的template；所以
在Template标签下有一个**ItemTemplate**标签来定义数据模板的样式。

####3.1 bindId
**bindId**实际上就是绑定数据的UI组件的id，我们通过bindId来识别具体的某一个绑定数据的UI组件，和组件id的功能类同但并不完全相同。前面我们已经描述过
数据模板针对ListView中的每个listitem定义其数据样式，即所有的item遵循一个模板，所以我们不能为每个UI组件设置属于其自己的id；即使在定义时为其设置了id，但是也不能
在.js文件中进行引用。UI组件的id主要功能是用来识别每个UI，但是在这种情况下我们已经不再需要通过id来识别每个UI，因为我们现在可以通过事件参数e和bindId来共同完成每个
UI组件的定位，具体使用方法我们会在下面的例子中见到。

####3.2 自定义数据模板
**自定义数据模板**根据不同的数据样式处理要求定义我们自己需要的数据模板，使用方法十分灵活。下面我们通过一个项目例子的中需求和代码来看看自定义数据模板需要如何定义：

![imageview](http://image.happysoft.cc)

上面这张动态演示图是我们需要通过ListView实现的UI效果图。对照着效果图，我们大致可以看出该页面的数据样式需求：

* 商品列表中含有两种不同的商品，一种为顶部大图模式，另一种为小图模式
* 每个ListItem中至有两个商品数据
* 每个商品数据包含图片、商品名称、价格、促销信息等数据
* 每个商品都能跳转到自己的淘宝店铺页面

这些需求基本上将我们上面描述过的数据模板问题都包含进来了：

* ① ListView中至少有两种数据块，即含有多个ListSection
* ② ListItem最小数据单元问题，这里的一个ListItem包含了两条数据元信息
* ③ ListItem中每个商品都有属于自己的定位(能被找到)，即能根据自身不同的属性点击跳转到自己的淘宝购买页

我们带着这些问题先从_.xml_文件看起，看看这种数据模板是如何定义的：

_example.xml：_

```xml
   code
```

首先我们看到，为了区别两种不同的商品，我们在ListView中声明了两个不同的ListSection，将顶部大图的
商品数据块和下面小图的商品数据块分开来(**tejia_products_section**/**other_products_section**)；并且定义了两种
不同的ItemTemplate(**tejia_products_template**/**other_products_template**)来分别处理两种不同的
商品数据样式，这样就解决了ListView中**_多个数据块以及数据块中多个不同的数据样式_**问题。

其次，在other_products_template中我们看到为了在ListItem中设置两个商品数据，我们在数据处理上定义了“**左边的商品/右边的商品**”两个
**view_block**。这样的处理方式在UI层面上至少区分了左/右两个商品的不同数据块，但实际上要在同一个ListItem中渲染多个数据块还是需要通过bindId
来解决；所以对于左/右两边不同的商品数据我们都定义了属于它们自己的bindId(**_left**/**_right**)。因此我们在处理复杂的逻辑数据结构的时候，可以
考虑这种在一个ListIem中插入多条数据的情况。

从上面我们可以知道，如果ListView中存在多个不同的数据块需求，我们可以通过定义不同的ListSection来解决；如果，某个数据块中存在多种不同的数据样式，那么我们
可以通过定义多个不同的ItemTemplate来解决这个问题。以上是在.xml文件中关于Template在UI层面上的处理，下面我们将要详细的介绍我们要如何将从远程获取的数据按照
已经我们定义好的数据模板来渲染数据。

_example.js：_

```js
   code
```

####3.3 ListView提供的模板
