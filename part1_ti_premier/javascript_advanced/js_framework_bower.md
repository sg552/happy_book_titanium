# 使用bower 管理 javascript, css...

1. 更新 npm

```bash
$ npm update -g bower
```

2. 

```bash
cd <your project> && bower init
```

```
{
  "name": "bestProjectEvar",
  "version": "1.2.3",
  "main": "./path/to/main.js",
  "dependencies": {
    "jquery": "~1.7.2"
  },
  "devDependencies": {
    "qunit": "1.10.0"
  },
  "ignore": [
    "the/most/useless/of/files.txt",
  ]
}
```

上面的文件中，bower只关心下面几个点：

- name: package的名字
- version: package的版本
- main: package中的主要文件
- dependencies: 各种依赖
- devDependencies: 开发时候的各种依赖
- ignore: 安装时忽略的文件

下面是几个命令：

- bower list 列出当前目录下安装好的package
- bower search <package_name> 搜索某个package
- bower info <package> 显示某个package的信息
- bower uninstall <package> 删除某个package
- bower install <package> 安装 

运行  `bower install <package>`之后， 就会发现在app 目录下下载了若干JS文件和目录

如果你希望更改的话，使用:

```javascript
// .bowerrc
{
  "directory": "app/assets/components"
}
```

