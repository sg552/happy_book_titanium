rails数据库迁移和model验证

一.rails 数据库迁移

由于需求变动，功能增加或者系统架构调整等种种原因，我们需要经常性的做数据库的迁移操作。在rails框架下，我们的数据库迁移工作会
由Active Record提供的一个功能，按照时间的顺序来管理数据库。在rails中，使用迁移我们无需编写SQL语句，只需要使用简单的Ruby DSL就能
够修改数据表，下面就是对Rails数据库迁移操作的一些简单介绍。

1.迁移简介

　　迁移使用一种简单且统一的方式来按照时间的先后顺序来修改我们的数据库。迁移使用Ruby DSL语言来完成，所以并不需要我们手动编写SQL语言去完成
对于我们使用的数据库种类和操作数据库的方式并不关心。你可以把每一次迁移看做一次数据库版本的改变。一开始的数据库什么都没有，每一次迁移我们都会
插入，修改或者删除其中的一些表，列或者字段。Active Record 知道怎样按照时间线来更新你的数据库，无论当前的数据库是什么状态，都能够更新到最新的
版本状态。Active Record 同时会更新你的 db/schema.rb文件匹配到最新的数据库结构。下面是一个数据库的例子：

创建好一个应用程序之后，执行下面的命令

   $ rake db:create 创建新的初始数据库

   $ rake db:migrate 执行数据库的初始迁移往数据库中增加初始的数据

2.创建迁移

  迁移会创建一个单独的文件存放在 db/migrate 目录下，每次迁移都会保存在一个独立的文件中。文件名的格式为：时间戳＋下划线分割的迁移文件名。时间戳的
格式为YYMMDDHHMMSS。下划线分割的迁移文件名要和迁移文件的类名相匹配，例如在20150901120000_create_products.rb文件中必须有一个类名为createProduct的类
，在20150901120001_add_details_to_products.rb文件中必须定义一个addDetailsToProducts的类。文件执行的先后顺序以及执行哪个迁移由时间戳来决定。这个在自
己生成迁移文件或者拷贝别的文件中的迁移文件时需要特别注意。

  2.1创建单独迁移
  自己计算时间戳并不是一件简单的事，好在rails的Active Record提供了一个自身的生成器，可以帮助我们来完成这个工作。
  $ rails generate migration AddPriceToProducts 这个命令会生成一个空的迁移文件，如下所示

  class AddPriceToProducts < ActiveRecord::Migration

    def change
    end
  end










二.model验证

   rails常用内建模型校验器
Ｒails自带有一套简单常用的模型校验器，使用这些我们可以完成大部分的基础的数据校验工作．
1.非空校验：validates_presence_of
2.唯一校验：validates_uniqueness_of
3.数据长度校验：validates_length_of
4.数值校验：vaildates_numericality_of
5.数据格式校验：validates_format_of
6.确认校验：validates_confirmation_of

首先假设我们拥有一个模型:Product,它包括有以下属性：name,catagory,price,

非空校验，商品名不为空
