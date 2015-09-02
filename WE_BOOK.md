# 敏捷移动端开发   -- 使用titanium, rails

TODO:
1. 制定目录
2. 分配写作内容
3. 整体统筹。
4. 找到编辑。出版。


目的：
1. 给新人培训用。 （几大本： RUBY/RAILS, TITANIUM, LINUX/git/vim)
2. 我们最好的名片， 要出书


参与人员： happy team 全体。

基于 Ti 4.0 SDK.  ( http://docs.appcelerator.com/platform/latest/#!/guide/Quick_Start)

## 目录

* 前言

### 第一部分 titanium 入门
* javascript 入门(高跃华) node 入门
* titanium 入门( titanium 的实质)（郭卫东）
* titanium & Alloy 中的各种UI的组件 (每人认领2个，加上图片示例）
  * ListView, Section, Item
  * Button
  * Label
  * ScrollView
  * TableView,
  * TextField
  * TextArea
  * TableGroup
  * TabGroup
  * 以及其他好多
（分配： 海洋： 0～A， 黄敏：B～iPad,  飞鹏： l ~ r , st： 张瑜， vw： 跃华。
Deprecated 的不用写。 例如：Ti.UI.TabbedBar , 转而写： Ti.UI.iOS.TabbedBar )


* Alloy 框架(胡飞鹏) 概述(胡飞鹏)
* Alloy View （各种插件，各种样式(tss)） (王涛)
* Alloy 中的各种事件（胡海洋）
* Alloy Controller (譞)
*（先不用,用得时候黄敏） Alloy Model, Alloy Data Binding 数据绑定, database
* Alloy 的debug (谁想起来就谁加）


### 第二部分 Titanium 进阶
*（先不用） Ti Module
* Alloy widget    (黄敏)
* 适配不同的机型  （张瑜）
* 使用i18n         （郭卫东）
* 发布（安卓，ios) （郭卫东）
* 集成web 页面    （黄敏）
* （先不用） 支付              （胡飞鹏）
* （先不用）分享（微信）(张瑜 安卓版)（郭卫东）
* （先不用）聊天 (文字，视频，语音）  (王涛)
* （先不用）第三方登录
* （先不用）地图
* （先不用）push
* 短信验证码(等等跃华）
* 调试UI (胡飞鹏) 使用自定义字体
* tishadow快速开发框架 （等等）
* jade/coffee/stss/grunt
* （先不用）tishadow unit test
* genymotion
* 动画 (胡海洋)
* debug, profiling
* 找到内存泄漏的地方
* 命令行?
* 使用经验谈


### 第三部分 rails 入门
* ruby 入门（大师）
* rails 入门(大师)
* 接口入门（双姐）
* Model 的可见性: 任意一个Model, 可以在整个Rails项目中的任何一个文件中调用. (浩浩)
* 数据库迁移， model验证，(李戈)
* 操作数据库, callbacks, 关联，查询(浩浩)
* 操作视图层, html.erb 文件(view) (明常)
* controller: 路由，action(浩浩)
* rails单元测试(大师)
* debug rails(全体,都可以把内容加进去)
* rails 命令行(彦民) http://guides.rubyonrails.org/command_line.html
* 部署rails (rails + thin, asset pipeline) (志文)
* 表单对象, rails view helper (大师)
### 第四部分 rails 进阶
* 再谈rails单元测试, 如何把握好测试的度 (高跃华)
* 使用selenium 进行自动化测试
* 使用chrome快速调试 web css 样式(胡飞鹏)
* 元编程（高跃华）
* 如何查看ruby/rails api
* 非常方便的方法（active support)
* 经验谈
* 使用缓存增加服务器的并发能力（apache ab, nginx )
* 配置nginx ，使用thin集群
* 大公司的运维配置
* 在优酷得到的教训
* 不要T皮球, 要与人为善。

### 第五部分 有用的工具，方法论

#### 职业规划,

* 必读书籍：
* 程序员的台阶很高(思路敏捷，清晰，表达沟通能力强，具备领导气质, 技术过硬）
* 程序员的十种去路
* 沟通最重要, 技术排第二。
* 收起你的个性，要谦虚，不要任性(控制好你的脾气)。
* 不要内向。内向的人是失败者。
* 不要踢皮球
* 要有个人的技术博客。 (黄敏)
* 有机会就要带领团队
* 架构，测试和运维不是正路。
* 每天都要学习，不要沦于平庸（买菜接孩子，算计各种羊毛）
* 创业团队务必有个靠谱的CTO
* 可以把任务分派出去，不要放在自己肩头硬抗，最后事情没做完，耽误了。
* 敏捷方法论
* 目前我很推崇的职业方向：新手 -> 熟手 -> 技术经理 -> CTO(创业)
* 多关注职业前辈的博客： robbin, gigix, iamhukai, 国外的：martin, kent,
* 使用最好的键盘，显示器。而不是一流的办公室，30块钱的破烂键盘鼠标。
* 办公室中的健康问题： 视力，脊柱，脾胃。 按时的离开显示器是为了更好的工作。
* 多参加程序员聚会，与人交流。

#### 技术建议
* 使用chrome 加快调试速度
* 敏捷方法论: 测试驱动，(难于测试的软件，就难于开发）
* 敏捷方法论: 极限编程
* 世界上只有三种编辑器：Vim , Emacs, 其他。(高跃华)
* 忘掉你的鼠标, 用好快捷键
* 使用编辑器时，最重要的一些快捷键
* SCM: 只用Git,  忘掉其他。
* 英语是提高个人能力的关键。 多读英文文档，多参与翻译，多贡献github, 多参加stackoverflow.(胡飞鹏)
* 频繁沟通才能保证项目失败，兼职的项目都会死掉。(胡飞鹏)
* 人跟人的能力不一样。
* 永远不要人肉重复。
* 命令行
* 放弃mac，使用linux.
* 技术很杂(好多列表，不要误以为一种技术通吃）， 入门用的技术(各种设计模式啥的）， 进阶：ThoughtWorks 技术雷达
* 对于ruby 程序员来说, 机器语言，汇编语言，object c 都是反人类的语言
* 招聘候选人时，务必识别项目毒药。
* 技术债是要命的, 代码，坏味道，
* 如何应对一句话需求, （inception 方法论)
* 团队内要及时传播知识。成为进取型团队（每个人都争先恐后的进步）
* 招人是个长期的任务，从头培养的人比高薪挖来的人好的多.
* 导致团队分崩离析的因素： 团队毒药，不公平的薪水，不开心的工作环境
