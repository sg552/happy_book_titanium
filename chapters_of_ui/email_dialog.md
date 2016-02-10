# EmailDialog

EmailDialog 可以让人直接写邮件。

![android](/images/ui_emaildialog_android.png)| ![ios](/images/ui_emaildialog_ios.png)| ![wp](/images/ui_emaildialog_wp.png)|
:---:|:-----:|:---:
Android|ios|Windows Phone

# 注意

- 必须用户提前在手机上登陆了邮箱，才能用。
- 在IOS 8.0及以上的模拟器不能通过测试，真机上可以。

# 例子

```js
var email_dialog = Ti.UI.createEmailDialog()
email_dialog.subject = "你好";
email_dialog.toRecipients = ['foo@sina.com'];
email_dialog.messageBody = '<b>Titanium 用起来不错啊!</b>';
var f = Ti.Filesystem.getFile('tokyo_cool.mp4');
email_dialog.addAttachment(f);
email_dialog.open();
```

