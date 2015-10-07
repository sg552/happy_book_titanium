
# 分页(Pagination)

## 介绍

在任何一个语言中，分页功能都是最重要的功能之一。

它的基本原理是： 给出第几页，每页多少条记录，就能在数据库中查找对应的记录。

在MySQL中，使用 limit + offset 关键字，  在其他数据库中也有对应的内容。

在2000年左右，曾经流行过一种分页方式：一次性读出所有的数据库记录，然后在前台决定是否展示。 不过由于这种方法在逻辑上是很低效的，所以我们一般不采纳。

在Rails2，3的时代，我们使用 will pagination, 在Rails3 之后，我们都使用Kaminari
( https://github.com/amatsuda/kaminari )

## 使用

假设我们在一个Rails3 的项目中：

修改 `Gemfile`: 
```
gem 'kaminari'
```

然后 ` $ bundle install`

例如，我们要按照每页 100条记录， 查找第二页的User内容：

```
users = User.page(2).per(100)
users.each do |user|
  puts "user: #{user.inspect}"
end
```

非常简单吧？ 上面的 users 是一个Array.

使用步骤：

1. 在View中：

```
<%= paginate @users %>
```
上述代码会产生一个分页的链接组，形如：  `« First ‹ Prev ... 2 3 4 5 6 7 8 9 10 ... Next › Last »`,  点击其中任意一页，就会跳转到形如：`/users?page=2`

2. 在controller中：

```
@users = User.page(params[:page]).per(100)
```
在 controller中，你也完全可以把per, page 与查询语句where ,order等混用：

```
@users = User.where('name like ?', '%jim%').order('name').page(params[:page]).per(100)
```

## 配置文件： config/initializers/

可以通过下列命令生成全局配置文件：
```bash
$ bundle exec rails g kaminari:config
```

该文件具体看起来是：

```ruby
default_per_page      # 25 by default
max_per_page          # nil by default
max_pages             # nil by default
window                # 4 by default
outer_window          # 0 by default
left                  # 0 by default
right                 # 0 by default
page_method_name      # :page by default
param_name            # :page by default
params_on_first_page  # false by default
```

你可以根据自己的喜好来修改。

## i18n

默认情况下，分页产生的链接形如： `first, previous`, 需要把它汉化，我们可以这样：

1. 设置rails的 locale是zh-CN
2. 在Rails.root/config/locales 中，增加一个语言文件(zh-CN.yml)

```yml
# 以下文件只是示例，不完整。
zh-CN:
  views:
    pagination:
      first: "&laquo; 首页"
      last: "末页 &raquo;"
      previous: "&lsaquo; 上页"
      next: "下页 &rsaquo;"
```

Karminari还有更多的作用，例如在Sinatra等框架中使用，为普通的Array做分页，针对Mongoid做分页等等。 具体请看官方文档。

