## 使用rpush的过程

http://yanmin.in/blog/rpush.html

这个东西，非常复杂，可以跟微信的支付、分享有的一拼。

需要：

1. pem 文件（apple 给的证书）

2. 这个证书，是development , 还是production   ( 是否是在sandbox中）

3. 在服务器端有代码( rails action ... ）

  3.1 需要几个表： apn_devices, rpush_apps, rpush_notifications

    apn_devices: 保存了，可以收到消息的设备的id

    rpush_apps: 保存？证书，环境，name，密码

    rpush_notifications: 保存 推送消息的正文

  3.2 在上面几个表中，要有数据（特别是 rpush_apps，部署好rails应用后，只运行一次就够了。)

  3.3 要有个 daemon : 每两秒钟，检查一下是否有消息要推送。

    $ bundle exec rpush start

  3.4 调试： 看log/rpush.log , 以及，看: rpush_notifications,中的 error_description信息。



4. 在客户端，有调用的代码。

  4.1 有调用代码

  4.2 要在实体机上测试

  4.3 运行之后，还必须 手动点击'允许接收消息'
