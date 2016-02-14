# 实战：Titanium中国开发者论坛App

我们要做一款真实的App. 不如就为Titanium中国开发者论坛做个App吧！躺在床上
还可以刷一刷屏，灌灌水~

特性如下：

- 有启动图，有个像样的图标
- 可以看到titanium 中国社区的分论坛(Forum)
- 点击任意分论坛后，可以看到该分类下所有话题(Topic)
- 点击任一标题，可以看到该话题下所有的帖子(Post)

## 需要的接口已经备好

- 看到所有的论坛

http://tidev.in/interface/forums

```
[
  {
    id: 1,
    name: "开发知识",
    description: " 大家关于开发的讨论"
  },
  {
    id: 2,
    name: "作品展示",
    description: "有哪些成功的Titanium作品，大家都发上来吧！ "
  },
  {
    id: 3,
    name: "其他话题",
    description: " 介绍，认识，线下活动，工作机会等。征基友也行。"
  }
]
```

- 看到某个论坛下所有的文章

需要的参数： forum_id （分论坛id)

http://tidev.in/interface/topics?forum_id=3

```
{
  forum_id: 3,
  forum_name: "其他话题",
  topics: [
    {
      title: "［北京］诚聘　titanium / ruby 全栈攻城狮 人数不限",
      topic_id: 13,
      user: "思维"
    },
    {
      title: "北京招聘titanium开发者",
      topic_id: 43,
      user: "思维"
    }
  ]
}
```


- 看到某个论坛下的所有文章

http://tidev.in/interface/posts?topic_id=64

需要的参数： topic_id (标题id)

```
{
  title: "明星框架 已经开源了",
  topic_id: 64,
  posts: [
  {
    html_body: "<p>欢迎大家多发 pull request:</p>
  <p>https://github.com/star-framework/star-framework</p>",
    user: "思维",
    created_at: "2016-02-10 07:30:38"
  }
  ]
}
```
