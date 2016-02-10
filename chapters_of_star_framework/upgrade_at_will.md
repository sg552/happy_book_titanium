# 在服务器端做控制，随时升级

想要升级，可以自动做，也可以手动做这个事儿。

原理：清除本地数据库的代码即可。

这样的话，用户再次打开app时，app 发现本地没有代码，就会向远程发起请求，
获取新的代码，并把新代码保存到本地数据库中。

```js
clean_cache = function() {
  Ti.App.db.execute("delete from jsons where json_type <> 'foo'");
};

```

## 自动做升级

在app 启动后，肯定要访问远程的接口，我们管这个接口叫 “初始化接口”，它会为
app提供各种初始化的参数。例如：

http://yourserver.com/interface/init.json:

```json
{
  app_version: '1.0.3'
}
```

当客户端获知该接口后，就会把这个 app_version 与本机保存的版本做比较，再决定
是否升级。

## 手动做升级

直接告诉你的用户，进入到“清空缓存”的页面，点击清空缓存，即可。
