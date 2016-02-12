# SystemButton

提供iOS标准的系统按钮。

大多数按钮常量可以通过`Button.systemButton`属性来为`NavigationBar`和
`ToolBar`定义系统图标。

在某些特定的场合，如TableViewRow中，可以使用`Button.style`来创建某些iOS标准按钮：
`CONTACT_ADD`,`DISCLOSURE`,`INFO_DARK`,`INFO_LIGHT`。

![System Button](/images/ui_ios_system_buttons.png)

- ACTION: action按钮，使用`Button.systemButton`来指定，只能被添加到`navigation bars`和`toolbars`中
- ACTIVITY: activity指示器，使用`Button.systemButton`来指定，可以被添加到`navigation bars`和`toolbars`中,当可见时，activity indicator就开始了
- ADD: 添加按钮，使用`Button.systemButton`来指定，只能被添加到`navigation bars`和`toolbars`中
- BOOKMARKS: 书签按钮，使用`Button.systemButton`来指定，只能被添加到`navigation bars`和`toolbars`中
- CAMERA: 相机按钮，使用`Button.systemButton`来指定，只能被添加到`navigation bars`和`toolbars`中
- CANCEL: 取消按钮，使用`Button.systemButton`来指定，只能被添加到`navigation bars`和`toolbars`中,按钮显示为本地化文字
- COMPOSE: 使用`Button.systemButton`来指定，只能被添加到`navigation bars`和`toolbars`中
- CONTACT_ADD: 使用`Button.style`来指定，不局限于`navigation bars`和`toolbars`中
- DISCLOSURE: 使用`Button.style`来指定，不局限于`navigation bars`和`toolbars`中

通过`Button.systemButton`指定的系统图标一般只能放在navigationBar中或者toolbar中，而`Button.style`指定的图标没有这个限制。

