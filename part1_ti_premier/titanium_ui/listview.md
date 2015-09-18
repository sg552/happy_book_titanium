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


    PS：如果你观察的够仔细的话，在浏览效果图时你应该会发现ListView中最后一条数据data 10是展示不完全的，ListView滑到底部
        松开后data 10会被屏幕遮挡一部分。这是ListView的一个小瑕疵，正是因为这个小瑕疵，所以当我们的数据size很大，超过屏
        幕长度时我们建议为ListView定义一个FooterView来解决这个问题。此时你可以只需要给这个FooterView定义一个空的任何UI
        组件就行了，它的作用只是为了占据一定的空间来保证我们数据展示的完整性，并没有实际意义。

我们上面介绍的是ListView的静态定义方法，其实更多的时候ListView都是动态定义出来的。因为数据更新的
需要我们无法明确数据的量度，因为需要在**.js**中根据远程获取的参数来动态定义，而这就需要绑定数据了。下
面我们将重点详细介绍ListView数据绑定时几个重要的属性及方法。

##ListView数据绑定

###1.1 ListSection
