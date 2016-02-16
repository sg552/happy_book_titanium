#ListView

ListView是最重要的组件之一，因其能灵活处理复杂的逻辑数据的绑定和更新，使其
成为UI组件中在处理大型的复杂的逻辑数据时最佳的UI组件选择项；
但与此同时它也成为最为复杂的UI组件之一。

如果你还从没接触过ListView，那么先看看下面的UI效果吧！

![listview](/images/listview_display1.gif)

从上面的效果图中我们可以看出ListView其实就是一个数据的“清单list”UI组件，
清单里的每条数据占据清单里的一行；并且当数据项超过屏幕长度时能自动滚动，
每条数据都有其各自的特性(效果图中点击每条数据弹出
的对话框内容可以看出)。下面是实现效果展示图的代码：

为了方便大家理解，我们这里使用Alloy 来表示：

my_list_view.xml:
```xml
<Alloy>
    <Window>
        <ListView id='my_list_view'>
            <ListSection>
                <HeaderView class='header_footer_view_style'>
                    <Label class='header_footer_label_style' text='HeaderView'/>
                </HeaderView>

                <ListItem title='data 1'/>
                <ListItem title='data 2'/>

                <!--此处省略data 3~data 18-->

                <ListItem title='data 19'/>
                <ListItem title='data 20'/>

                <FooterView/>
            </ListSection>
        </ListView>
    </Window>
</Alloy>
```

my_list_view.tss:

```tss
'#my_list_view':{
  top:'0',
  width:'100%',
  height:'100%'
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

controller:
```js
$.my_list_view.addEventListener('itemclick',function(e){
  alert('数据排列序号：'+e.itemIndex);
});
```

从my_list_view.xml文件中，我们可以大致的看出ListView总共由三部分组成：

- HeaderView: ListView的head头部控件，可以在这里定义头部的样式
- ListSection: LisiView的body身体部分，数据都展示在这里
- FooterView: ListView的foot，定义尾部样式

一般情况下，除非需要用到HeaderView与FooterView，
否则ListView的头部、尾部样式可以不定义，不影响整个UI效果。

除此之外，ListView还可以在顶部(HeaderView上方)嵌套一个搜索栏，
用于对数据的筛选显示。

不过，对于Android与IOS分别有不同的UI组件：

- SearchBar，适用于IOS；
- Ti.UI.Android.SearchView，适用于Android；

如果你观察仔细的话，在浏览效果图时你应该会发现ListView中最后一条数据
data 20是展示不完全的，ListView滑到底部松开后data 20会被屏幕遮挡一部分。

这是ListView的一个小瑕疵，正是因为这个小瑕疵，所以当我们的数据size很大，
超过屏幕长度时我们建议为ListView定义一个FooterView来解决这个问题。

此时你可以只需要给这个FooterView定义一个空的任何UI组件就行了，
它的作用只是为了占据一定的空间来保证我们数据展示的完整性，并没有实际意义。

我们上面介绍的是ListView的静态定义方法，其实更多的时候ListView都是动态定义出来的。因为数据更新的
需要我们无法明确数据的量度，因此需要在_.js_中根据远程获取的参数来动态定义，而这就需要绑定数据了。下
面我们将重点详细介绍ListView数据绑定时几个重要的属性及方法。

## 数据绑定

说通俗一些，就是把数据放到ListView中去。

### 注意

ListView中的template中，只能出现下面的UI类型：

- Titanium.UI.ActivityIndicator
- Titanium.UI.Button
- Titanium.UI.ImageView
- Titanium.UI.Label
- Titanium.UI.ProgressBar
- Titanium.UI.Slider
- Titanium.UI.Switch
- Titanium.UI.TextArea
- Titanium.UI.TextField

###1. ListSection

ListSection是ListView的核心部分，处理数据的绑定和渲染等。

在ListView中，ListSection区分不同的数据块(section本身就有区域的意思)，
定义了多少个ListSection就有多少个数据块；需要往哪个数据块渲染数据，
则指定该ListSection的id进行渲染即可。

####1.1 Sections

sections是ListView的ListSection的集合，通过getSections()方法获取，
返回数组型数据集合。该属性最重要的用法不在获取ListView的sections的数据集合上，
而是在动态创建时用来渲染ListView的ListSection的数据，
即setSections()方法的使用。

我们已经知道getSections()方法返回的是sections数组型集合数据，
那么setSections()方法就是绑定一个数组型的集合数据了。
因此我们可以通过创建一个关于ListSection的多条数据的数组集合,
来渲染ListView的多个ListSection。

下面是参考代码：

```js
//headerTitle是ListSection的一个属性porperty
var my_list_sections_data = [
  {
    properties:{
      headerTitle: 'Data Section 1'
    }
  },
  {
    properties:{
      headerTitle: 'Data Section 2'
    }
  }
]

$.my_list_view.setSections(my_list_sections_data);

var my_list_view_sections_length = $.my_list_view.getSections();

console.info(my_list_view_sections_length) //输出结果为2
```

####1.2 sectionIndex

sectionIndex描述ListView中每个ListSection的序号index，从0开始。
该属性的获取的方法一般不能直接获取，而需要通过事件参数e来获得。

我们通过sectionIndex来确定ListView中某个确定的ListSection，进而
能够获取到该ListSection中具体的某一个ListItem的数据。

具体代码参考如下：

```js
//假设我们要获取某个ListSection中的某个ListItem中绑定数据
(绑定的id为bind_color，设置为red)的label的颜色属性

$.my_list_view.addEventListener('itemclick',function(e){
  var label_color =
    $.my_list_view.sections[e.sectionIndedx].items[e.itemIndex].bind_color.color;

  console.info(label_color);  // =>  'red'
});

```

itemclick为ListView的点击监听事件，
点击某个listItem并通过事件参数e我们可以获取到该ListItem所在的ListSection
(e.sectionIndex)，以及是该ListSection中哪一个ListItem(e.itemIndex)；
再通过绑定的id获取该label的颜色属性。

通过上面的代码，我们现在能进一步获取ListView中的数据了。关于ListItem、items、itemIndex的使用，我们下面将详细介绍。

###2. ListItem

ListItem是ListView的数据单元，在ListView中一行即是一个ListItem；
但这并不意味着ListItem中所包含的就是最小的数据单元，
因为一个ListItem中可能包含多条数据。(这需要通过数据模板Template来实现，
不同的数据模板数据单元的划分也不同)但是进行数据渲染时，
最小的渲染数据单元就是ListItem；并且ListView的点击监听事件也是加在ListItem上，
当然你也可以为ListItem中的某个特定的数据设置特有的点击事件，两者并不冲突。

####2.1 Items

items是ListSection中所有ListItem的集合，类似sections。
获取方法以及设置方法也与sections类似，getItems()获取某ListSection中所有
ListItem的集合，返回数组型数据；
setItems()则为某个ListSection绑定一个数组型的ListItem数据。

```js
var my_list_items_data = [
  {
    properties:{
      title:'标题1'
    }
  },
  {
    properties:{
      title:'标题2'
    }
  },
]

$.my_list_section.setItems(my_list_items_data);

var my_list_section_items_length = $.my_list_section.getItems();

//输出结果为2
console.info(my_list_section_items_length)
```

####2.2 itemIndex

itemIndex描述ListSection中每个LisetItem的序号index，从0开始，
和sectionIndex类似。同样可以通过事件参数e来获取，参考sectionIndex。

通过上面的介绍我们已经大致了解了ListView获取数据的方法，
要获取ListItem中的某个数据，我们要知道该数据在ListSection中的位置；
知道ListItem的位置之后，我们还要获取该ListSection在LisView中的位置；
只有这样我们才能精确获取该数据的具体位置。

事实上，在开发中我们很少去动态创建ListSection；即一个页面的数据块的分类一般情况下是已经确定的，
即使在不确定的情况下我们只要在逻辑代码中考虑一下该ListSection没有数据的情况。
(如果该ListSection有样式需求，如有headerTitile标题，
没有数据的情况下是不能显示该标题的(或者其他的特殊处理)；
那么我们就必须得动态定义该ListSection了)。

其实，真正需要慎重考虑的是我们对ListItem中数据的处理；
即我们是否能设计一个比较好的数据模板来处理比较复杂的数据需求；
接下来我们重点介绍数据模板Template。

###3. 数据模板Template
Template数据模板描述的是ListView在渲染数据时，数据渲染所要遵循的“渲染样式”，即数据在LisView中的结构样式，说白了就是设定好
所要的UI样式，然后将数据绑定到相关的UI组件上。数据渲染主要通过bindId来实现，即绑定id的UI组件；该组件即用来渲染其对应的数据。
在ListView中，我们可以通过定义Template标签来实现；我们所定义的数据样式，其实就是对ListItem中所要填充的数据进行样式定义，即item的template；所以
在Template标签下有一个ItemTemplate标签来定义数据模板的样式。

####3.1 bindId
bindId实际上就是绑定数据的UI组件的id，我们通过bindId来识别具体的某一个绑定数据的UI组件，和组件id的功能类同但并不完全相同。前面我们已经描述过
数据模板针对ListView中的每个listitem定义其数据样式，即所有的item遵循一个模板，所以我们不能为每个UI组件设置属于其自己的id；即使在定义时为其设置了id，但是也不能
在.js文件中进行引用。UI组件的id主要功能是用来识别每个UI，但是在这种情况下我们已经不再需要通过id来识别每个UI，因为我们现在可以通过事件参数e和bindId来共同完成每个
UI组件的定位，具体使用方法我们会在下面的例子中见到。

####3.2 自定义数据模板
自定义数据模板根据不同的数据样式处理要求定义我们自己需要的数据模板，使用方法十分灵活。下面我们通过一个项目例子的中需求和代码来看看自定义数据模板需要如何定义：

![](/images/listview_display2.gif)

上面这张动态演示图是我们需要通过ListView实现的UI效果图。对照着效果图，我们大致可以看出该页面的数据样式需求：

 商品列表中含有两种不同的商品，一种为顶部大图模式，另一种为小图模式
 每个ListItem中至有两个商品数据
 每个商品数据包含图片、商品名称、价格、促销信息等数据
 每个商品都能跳转到自己的淘宝店铺页面

这些需求基本上将我们上面描述过的数据模板问题都包含进来了：

 ① ListView中至少有两种数据块，即含有多个ListSection
 ② ListItem最小数据单元问题，这里的一个ListItem包含了两条数据元信息
 ③ ListItem中每个商品都有属于自己的定位(能被找到)，即能根据自身不同的属性点击跳转到自己的淘宝购买页

我们带着这些问题先从_.xml_文件看起，看看这种数据模板是如何定义的：

_example.xml：_

```xml
<ListView id="mall_materials_page">
  <Templates>
    <!--特价商品ItemTemplate-->
    <ItemTemplate name="tejia_products_template" height="185" backgroundColor="#efedef">
      <View zIndex="0" bindId="tejia_product_view_block">
        <View id="tejia_product_info_view_block">
          <!--促销价-->
          <Label id="tejia_product_hot_selling_price_style" bindId="tejia_product_hot_selling_price"/>
          <!--市场价-->
          <Label id="tejia_product_original_price_style" bindId="tejia_product_original_price"/>
          <!--卖出件数-->
          <Label id="tejia_product_sold_num_style" bindId="tejia_product_sold_num"/>
          <!--卖出件数text-->
          <Label id="tejia_product_sold_num_text" text="人已买"/>
          <!--剩余时间title-->
          <Label id="tejia_product_left_time_title" text="距结束仅剩"/>
          <!--剩余天数-->
          <Label class="tejia_product_left_time_style" left="67%" bindId="tejia_product_left_time_day"/>
          <!--剩余天数text-->
          <Label class="tejia_product_left_time_text" left="74.8%" text="天"/>
          <!--剩余小时-->
          <Label class="tejia_product_left_time_style" left="81%" bindId="tejia_product_left_time_hour"/>
          <!--剩余小时text-->
          <Label class="tejia_product_left_time_text" left="89.5%" text="小时"/>
        </View>
    </ItemTemplate>

    <!--其他商品ItemTemplate-->
    <ItemTemplate name="other_products_template" height="175" backgroundColor="#efedef">
      <!--左边的商品-->
      <View class="other_product_view_block" left="0" bindId="other_product_view_block_left">
        <ImageView class="other_product_image" bindId="other_product_image_left"/>
        <Label class="other_product_name" bindId="other_product_name_left"/>
        <Label class="other_product_original_price" bindId="other_product_original_price_left"/>
        <Label class="other_product_jinsheng_text" bindId="other_product_jinsheng_text_left" text="仅剩"/>
        <Label class="other_product_left_time_day" bindId="other_product_left_time_day_left"/>
        <Label class="other_product_left_time_day_text" bindId="other_product_left_time_day_text_left" text="天"/>
        <Label class="other_product_left_time_hour" bindId="other_product_left_time_hour_left"/>
        <Label class="other_product_left_time_hour_text" bindId="other_product_left_time_hour_text_left" text="小时"/>
        <Label class="other_product_hot_selling_price" bindId="other_product_hot_selling_price_left"/>
        <Label class="other_product_hot_selling_price" bindId="other_product_store_price_left"/>
        <Label class="other_product_sold_num" bindId="other_product_sold_num_left"/>
        <Label class="other_product_sold_num_text" text="已售出"/>
      </View>

      <!--右边的商品-->
      <View class="other_product_view_block" right="0" bindId="other_product_view_block_right">
        <ImageView class="other_product_image" bindId="other_product_image_right"/>
        <Label class="other_product_name" bindId="other_product_name_right"/>
        <Label class="other_product_original_price" bindId="other_product_original_price_right"/>
        <Label class="other_product_jinsheng_text" bindId="other_product_jinsheng_text_right" text="仅剩"/>
        <Label class="other_product_left_time_day" bindId="other_product_left_time_day_right"/>
        <Label class="other_product_left_time_day_text" bindId="other_product_left_time_day_text_right" text="天"/>
        <Label class="other_product_left_time_hour" bindId="other_product_left_time_hour_right"/>
        <Label class="other_product_left_time_hour_text" bindId="other_product_left_time_hour_text_right" text="小时"/>
        <Label class="other_product_hot_selling_price" bindId="other_product_hot_selling_price_right"/>
        <Label class="other_product_hot_selling_price" bindId="other_product_store_price_right"/>
        <Label class="other_product_sold_num" bindId="other_product_sold_num_right"/>
        <Label class="other_product_sold_num_text" text="已售出"/>
      </View>
    </ItemTemplate>

    <ListSection id="tejia_products_section"/>
    <ListSection id="other_products_section"/>
</ListView>
```

首先我们看到，为了区别两种不同的商品，我们在ListView中声明了两个不同的ListSection，将顶部大图的
商品数据块和下面小图的商品数据块分开来(tejia_products_section/other_products_section)；并且定义了两种
不同的ItemTemplate(tejia_products_template/other_products_template)来分别处理两种不同的
商品数据样式，这样就解决了ListView中_多个数据块以及数据块中多个不同的数据样式_问题。

其次，在other_products_template中我们看到为了在ListItem中设置两个商品数据，我们在数据处理上定义了“左边的商品/右边的商品”两个
view_block。这样的处理方式在UI层面上至少区分了左/右两个商品的不同数据块，但实际上要在同一个ListItem中渲染多个数据块还是需要通过bindId
来解决；所以对于左/右两边不同的商品数据我们都定义了属于它们自己的bindId(_left/_right)。因此我们在处理复杂的逻辑数据结构的时候，可以
考虑这种在一个ListIem中插入多条数据的情况。

从上面我们可以知道，如果ListView中存在多个不同的数据块需求，我们可以通过定义不同的ListSection来解决；如果，某个数据块中存在多种不同的数据样式，那么我们
可以通过定义多个不同的ItemTemplate来解决这个问题。以上是在.xml文件中关于Template在UI层面上的处理，下面我们将要详细的介绍我们要如何将从远程获取的数据按照
已经我们定义好的数据模板来渲染数据。

_example.js：_

```js
//以下代码为简化后的核心代码

//获取远程商品数据
request_for_mall_materials_page_data = function() {
  var mall_materials_page_client, request_for_mall_materials_page_data_url;
  mall_materials_page_client = Ti.Network.createHTTPClient({
    onreadystatechange: function() {
      if (is_data_exist === false) {
        return load();
      }
    },
    onload: function() {
      mall_materials_page_data = JSON.parse(this.responseText);
      if (mall_materials_page_data.length === 0) {
        toast('抱歉，没有找到相关的商品！', $.mall_materials_page_data);
      }
      else {
        is_data_exist = true;

        //特价商品数据
        tejia_products_data = mall_materials_page_data.tejia_products;
        //其他商品数据
        other_products_data = mall_materials_page_data.other_products;

        products_initial();
      }
      return load_cancel();
    },
    onerror: function() {
      load_cancel();
      toast('获取数据失败，请检查当前的网络设置！', $.mall_materials_page);
      return is_data_exist = false;
    }
  });

  request_for_mall_materials_page_data_url = Settings_mall.server + '/interface/mall_products/jia_ju_guang_products';
  mall_materials_page_client.open('GET', request_for_mall_materials_page_data_url);

  return mall_materials_page_client.send();
};

//特价商品数据渲染
tejia_products_initial = function() {
  var count;
  tejia_products_bind_data = [];

  count = 0;
  while (count < tejia_products_data.length) {
    tejia_products_data_bind(count);
    count++;
  }
  return $.tejia_products_section.setItems(tejia_products_bind_data);
};

//其他商品数据渲染
other_products_initial = function(length) {
  var count;
  other_products_bind_data = [];

  count = 0;
  while (count < length / 2) {
    other_products_data_bind(count);
    count++;
  }
  return $.other_products_section.setItems(other_products_bind_data);
};

//特价商品绑定数据
tejia_products_data_bind = function(count) {
    return tejia_products_bind_data.push({
      template: 'tejia_products_template',
      properties: {
        selectionStyle: Ti.UI.iPhone.ListViewCellSelectionStyle.NONE
      },

      //特价商品图片
      tejia_product_view_block: {
        index: tejia_products_data[count].url,
        backgroundImage: tejia_products_data[count].cover
      },
      //特价商品促销价
      tejia_product_hot_selling_price: {
        text: '￥' + tejia_products_data[count].sale_price
      },
      //特价商品原价
      tejia_product_original_price: {
        text: '￥' + tejia_products_data[count].market_price,
        backgroundImage: '/images/delete_line_white.png'
      },
      //特价商品售出件数
      tejia_product_sold_num: {
        text: tejia_products_data[count].sales_volume
      },
      //特价商品促销剩余时间--天
      tejia_product_left_time_day: {
        text: tejia_products_data[count].finish_day
      },
      //特价商品促销剩余时间--小时
      tejia_product_left_time_hour: {
        text: tejia_products_data[count].finish_hour
      }
    });
};

//其他商品绑定数据
other_products_data_bind = function(count) {
    return other_products_bind_data.push({
      template: 'other_products_template',
      properties: {
        selectionStyle: Ti.UI.iPhone.ListViewCellSelectionStyle.NONE
      },

      //左边的商品
      other_product_image_left: {
        index: other_products_data[count  2].url,
        image: other_products_data[count  2].cover
      },
      other_product_name_left: {
        text: other_products_data[count  2].name
      },
      other_product_original_price_left: {
        text: '￥' + other_products_data[count  2].market_price,
        backgroundImage: '/images/delete_line.png'
      },
      other_product_jinsheng_text_left: {
        visible: other_products_data[count  2].sale_or_not
      },
      other_product_left_time_day_left: {
        visible: other_products_data[count  2].sale_or_not,
        text: other_products_data[count  2].finish_day
      },
      other_product_left_time_day_text_left: {
        visible: other_products_data[count  2].sale_or_not
      },
      other_product_left_time_hour_left: {
        visible: other_products_data[count  2].sale_or_not,
        text: other_products_data[count  2].finish_hour
      },
      other_product_left_time_hour_text_left: {
        visible: other_products_data[count  2].sale_or_not
      },
      other_product_hot_selling_price_left: {
        visible: other_products_data[count  2].sale_or_not,
        text: '￥' + other_products_data[count  2].sale_price
      },
      other_product_store_price_left: {
        visible: !other_products_data[count  2].sale_or_not,
        text: '￥' + other_products_data[count  2].price
      },
      other_product_sold_num_left: {
        text: other_products_data[count  2].sales_volume
      },

      //右边的商品
      other_product_image_right: {
        index: other_products_data[(count  2) + 1].url,
        image: other_products_data[(count  2) + 1].cover
      },
      other_product_name_right: {
        text: other_products_data[count  2 + 1].name
      },
      other_product_original_price_right: {
        text: '￥' + other_products_data[count  2 + 1].market_price,
        backgroundImage: '/images/delete_line.png'
      },
      other_product_jinsheng_text_right: {
        visible: other_products_data[count  2 + 1].sale_or_not
      },
      other_product_left_time_day_right: {
        visible: other_products_data[count  2 + 1].sale_or_not,
        text: other_products_data[count  2 + 1].finish_day
      },
      other_product_left_time_day_text_right: {
        visible: other_products_data[count  2 + 1].sale_or_not
      },
      other_product_left_time_hour_right: {
        visible: other_products_data[count  2 + 1].sale_or_not,
        text: other_products_data[count  2 + 1].finish_hour
      },
      other_product_left_time_hour_text_right: {
        visible: other_products_data[count  2 + 1].sale_or_not
      },
      other_product_hot_selling_price_right: {
        visible: other_products_data[count  2 + 1].sale_or_not,
        text: '￥' + other_products_data[count  2 + 1].sale_price
      },
      other_product_store_price_right: {
        visible: !other_products_data[count  2 + 1].sale_or_not,
        text: '￥' + other_products_data[count  2 + 1].price
      },
      other_product_sold_num_right: {
        text: other_products_data[count  2 + 1].sales_volume
      }
    });
};
```
从_example.js_给出的代码我们可以看出，整个页面数据绑定可以分为三大块：获取远程数据、特价商品数据
绑定/渲染以及其他商品数据绑定/渲染。

① 获取远程数据

页面向后台发起url请求获取该页面的所有商品数据mall_materials_page_data，如果获取成功我们将“特价
商品数据tejia_products_data”和“其他商品数据others_products_data”从数据中分离出来；这个过程通过函数request_for_mall_materials_page_data()
来处理。

② 数据绑定

获取了远程数据之后，我们开始绑定数据。首先我们需要将绑定的数据临时存储在一个数组中，为了以后的数据渲染做准备；我们分别创建了两个临时存储的绑定数据的数组
tejia_products_bind_data[]和other_products_bind_data[]，然后就可以开始绑定数据了。绑定数据的过程发生在tejia_products_data_bind()和other_products_data_bind()两个函数中，
我们详细的来看看这两个函数是如何完成“数据绑定”的：(由于该两个函数的绑定数据方式类同，我们other_products_data_bind()为例)

[1]other_products_bind_data.push({})：这个方法是数据绑定的主体，即我们将需要绑定的数据存入push()我们创建的两个临时数组中

[2]template: 'other_products_template'：这个属性选择我们绑定数据所要使用的“数据模板”，即我们在_.xml_文件中定义好的数据模板；这里我们需要对除顶部特价商品外的其他商品进行数据绑定，因此我们选择其他商品的数据模板other_products_template

[3]properties：这个属性用来定义一些关于listItem所需要的样式，具体情况具体声明(代码中的properties定义了listItem点击选中效果的样式为空，即不使用listItem默认的点击选中效果)

[4]other_product_image_left：如果你细心观察的话，接下来的所有的这些以_left/_right结尾的属性其实都是我们在_.xml_文件中已经定义好的bindId，即那些需要绑定数据的UI组件；这也就是真正的数据绑定的核心内容，为这些UI组件渲染从远程获取到的数据。我们以第一条数据绑定为例，来看看数据绑定的具体过程：

   <1>首先，我们可以看到所有的数据绑定都是以key:value的形式进行数据绑定的

   <2>index：这个属性其实并不属于imageView的定义属性(所谓的定义属性是指在API中UI定义的
   properties，如：imageView有image属性，label有text属性[下一条的数据绑定就是label绑定text数据])，事
   实上它是动态数据绑定时可以添加的一个序号属性，并没有太大的实际意义；但是我们可以利用它来解决一
   些很麻烦的问题。(如：在这个我们所要实现的UI效果中需要点击商品图片跳转到其淘宝购买页面，这需要一
   个url参数来解决问题；可是这个url参数该怎么存储，存储到哪里去呢？因为imageView本身并没有一个这样
   的属性来存储它所关联的url，所以我们必须的通过其他方式来达到这个目的，而为其设置index来存储这个
   url信息则很好的解决了这个问题。)

   <3>image：这个属性即是该商品的图片数据key，它所绑定的value为other_products_data[count  2].cover
   则是从远程获取的该商品图片的url数据。(数组中的序号参数count2以及下面的数组序号参
   数count2+1分别对应listItem中“左边/右边”的商品数据，即左边的商品则绑定数据中偶数序的商品数据，右
   边的商品则绑定商品数据中奇数序的商品数据；这样处理之后才使得商品数据按照“左/右”的“偶/奇”顺序绑定在listItem中，这也是实现
   一个listItem中插入多条数据的方式之一。)

③ 数据渲染

数据绑定完毕之后，即通过函数tejia_products_data_bind()/other_products_data_bind()向临时数组tejia_products_bind_data[]/other_products_bind_data[]中存入相关的
商品数据之后，我们需要将这些数据渲染到与之对应的listSection的listItem中。如果你没忘记的话，应该还记得我们在介绍ListSection和ListItem时其实就已经提到了使用方法。
要往对应的listItem中渲染对应的数据，我们需要先找到该listItem所在的listSection，而listSection则可以直接通过$.的形式来获取；接下来就是使用listSection的方法setItems()就行了，
所以最终的结果是：tejia_products_section渲染tejia_products_bind_data数据的方法为“$.tejia_products_section.setItems(tejia_products_bind_data);”，other_products_section渲染other_products_bind_data数据
的方法为“$.other_products_section.setItems(other_products_bind_data);”。

通过的上面的介绍，我们对listView的数据绑定和渲染过程已经有了一个较详细的了解过程了，接下来还剩下“商品的点击跳转到其淘宝购买页面”这个功能块没有介绍。下面我通过该项目中的代码开始详细介绍这个功能块：

```js
$.mall_materials_page.addEventListener('itemclick', function(e) {
  var go_tao_bao, url;

  //特价商品跳转到淘宝
  if (e.bindId === 'tejia_product_view_block') {
    url = $.tejia_products_section.items[e.itemIndex].tejia_product_view_block.index;

    go_tao_bao = Alloy.createController("taobao_webview", {
      url: url
    }).getView();

    go_tao_bao.setLeft('100%');
    return go_tao_bao.open(slide_to_left);
  }

  //其他商品跳转到淘宝
  else if (e.bindId === 'other_product_image_left') { //左边的商品跳转到淘宝
    url = $.other_products_section.items[e.itemIndex].other_product_image_left.index;

    go_tao_bao = Alloy.createController("taobao_webview", {
      url: url
    }).getView();

    go_tao_bao.setLeft('100%');
    return go_tao_bao.open(slide_to_left);
  }
  else if (e.bindId === 'other_product_image_right') { //右边的商品跳转到淘宝
    url = $.other_products_section.items[e.itemIndex].other_product_image_right.index;

    go_tao_bao = Alloy.createController("taobao_webview", {
      url: url
    }).getView();

    go_tao_bao.setLeft('100%');
    return go_tao_bao.open(slide_to_left);
  }
});
```

这个功能其实就是我们上面提到过的如何通过事件参数e以及bindId来在listView中定位到某个listItem中的数
据的方法实现。

① itemclick事件

这个效果是建立在listView的点击监听事件itemclick下的，因为我们要获取事件参数e；只有获取到了e我们
才能通过e获取得到e中的相关信息(这里我们获取bindId信息)。

② bindId定位绑定数据的UI

获取了事件参数e之后，我们从e中得到我们需要的bindId信息，通过bindId我们就已经准确知道了我们需要定位的
UI组件了。如果仅仅如此，我们还不能完全获取到某一个具体位置的UI数据信息，因为每一个listItem中UI的bindId
都相同；因此我们还需要知道该绑定数据的UI所在的listItem的位置信息。

③ itemIndex最终定位listItem的绝对位置

通过itemIndex得到listItem的定位信息，我们在介绍listItem时就已经提到过相关内容了；这里我们要介绍的是通过bindId
来获取该绑定数据UI组件的属性key，从而获取到这个key的value信息。还记得我们在数据绑定中提到的index属性吗？我们
就以这个为例子来看看是如何实现的：

    url = $.other_products_section.items[e.itemIndex].other_product_image_left.index;

前面已经提到过，要跳转到某“商品的其淘宝购买页面”，我们需要该页面的url信息；我们已经通过index属性存储了该url，那么
我们现在只要获取到该url再打开url所链接到的页面就行了。要获取到该index(key)中的url(value)，我们必须要知道我们是否点
击到了该商品图片，所以我们需要通过if条件语句来判断：else if(e.bindId === 'other_product_image_left')，即如果
点击的图片位于该listItem中的左边，即需要跳转到
listItem中左边的商品的淘宝购买页面(右边的商品则判断bindId是否为other_product_image_right)。这样我就完成了这个点击跳转
的效果。

以上所述是ListView自定义数据模板在项目中的一个实例。ListView自定义数据模板的灵活性体现在UI效果的需求不同上，不同的UI效果需求
对应的数据模板可能完全不同，但是他们都有着一样的逻辑处理过程；并且其数据绑定和渲染方式以及UI的定位方法大同小异。掌握这些方法，
那么ListView自定义数据模板就不困难！不过，自定义数据模板是在ListView本身提供的默认的数据模板不能满足自己的UI效果需求时需要考虑的
方法，如果ListView本身提供的默认的数据模板能满足需求，我们就没必要如此麻烦自己定义数据模板。下面我们来简单介绍一下ListView的默认
数据模板。

####3.3 ListView的默认模板

我们先看看ListView默认数据模板的样式(这里引用API例子)：

![imageview](http://docs.appcelerator.com/platform/latest/images/download/attachments/40928632/01_iphone_image.png)

下面是样式的_.xml_/_.tss_参考代码：

```xml
<Alloy>
    <Window class="container">
        <ListView id="elementsList">
            <ListSection name="elements">
                <ListItem title="Hydrogen" image="icons/Hydrogen.png"/>
                <ListItem title="Helium" image="icons/Helium.png"/>
                <ListItem title="Lithium" image="icons/Lithium.png"/>
                <ListItem title="Beryllium" image="icons/Beryllium.png"/>
                <ListItem title="Boron" image="icons/Boron.png"/>
                <!--以下省略-->
            </ListSection>
        </ListView>
    </Window>
</Alloy>
```

```tss
//这里的样式文件没有通过class/id来定义，而是直接使用UI组件的名称来定义；这是允许的，不过这种方法等同于class效果

"ListItem": {
  accessoryType: Titanium.UI.LIST_ACCESSORY_TYPE_DISCLOSURE
}
```

通过上面的代码，我们知道在默认的情况下，不定义template标签，只要在listLitem中声明相关的属性；那么，listView最终展现的效果
就会以默认模板的样式展现。这里的默认模板样式包括(listItem中需要声明的属性，如果不声明或缺失，那么相关的组件将不会显示；并且
可能得不到默认的模板效果)：listItem的标题
title，图片image以及一个由listItem样式(.tss文件定义)定义的“右箭头”(即右边的可点击拓展图标)标识。

如果默认模板的样式能满足你的UI需求，那么就使用这种样式吧！如果，需要动态绑定数据，那么我们同样可以为这些listItem定义bindId来实现
动态绑定数据。以上是本章对listView的介绍，重点介绍了listView动态绑定数据的方法，如果需要更加详细的介绍可以参考官方文档：http://docs.appcelerator.com/platform/latest/#!/guide/Alloy_ListView_Guide
