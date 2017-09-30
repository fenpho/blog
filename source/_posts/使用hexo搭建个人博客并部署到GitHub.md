---
title: 使用hexo搭建个人博客并部署到GitHub
date: 2017-09-30 18:06:41
categories:
	- Git && GitHub 
tags:
	- Git
	- hexo
	- GitHub
	- 个人博客
---
### 1、什么是 Hexo？
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
### 2、准备工作
#### 2.1 安装Git
> **Mac 用户**您在编译时可能会遇到问题，请先到 App Store 安装 Xcode，Xcode 完成后，启动并进入 **Preferences -> Download -> Command Line Tools -> Install** 安装命令行工具。

[](https://hexo.io/zh-cn/docs/#安装-Git)安装 Git
Windows：下载并安装 [git](https://git-scm.com/download/win).
Mac：使用 [Homebrew](http://mxcl.github.com/homebrew/), [MacPorts](http://www.macports.org/) ：`brew install git` 或下载 [安装程序](http://sourceforge.net/projects/git-osx-installer/) 安装。
Linux (Ubuntu, Debian)：`sudo apt-get install git-core`
Linux (Fedora, Red Hat, CentOS)：`sudo yum install git-core`

> **Windows 用户**由于众所周知的原因，从上面的链接下载git for windows最好挂上一个代理，否则下载速度十分缓慢。也可以参考[这个页面](https://github.com/waylau/git-for-win)，收录了存储于百度云的下载地址。

#### 2.2安装 Node.js
安装 Node.js 的最佳方式是使用 [nvm](https://github.com/creationix/nvm)。
cURL:
`$ curl https://raw.github.com/creationix/nvm/master/install.sh | sh`
Wget:
`$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh`
安装完成后，重启终端并执行下列命令即可安装 Node.js。
`$ nvm install stable`

或者您也可以下载 [安装程序](http://nodejs.org/) 来安装。
> **Windows 用户**
对于windows用户来说，建议使用安装程序进行安装。安装时，请勾选**Add to PATH**选项。另外，您也可以使用**Git Bash**，这是git for windows自带的一组程序，提供了Linux风格的shell，在该环境下，您可以直接用上面提到的命令来安装Node.js。打开它的方法很简单，在任意位置单击右键，选择“Git Bash Here”即可。由于Hexo的很多操作都涉及到命令行，您可以考虑始终使用**Git Bash**来进行操作。

### 3、安装hexo
执行以下命令：
`$ npm install -g hexo-cli`
安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。
```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

新建完成后，指定文件夹的目录如下：
├── _config.yml
├── package.json
├── scaffolds
├── source
 | ├── _drafts
 | └── _posts
└── themes
接下来要做的就是修改配置文件了，在根目录下找到文件：_config.yml
安装自己的需要进行修改，一般修改下网站标题，作者就可以了
```
# Site
title: Fenpho  //网站标题
subtitle: //网站副标题
description://网站描述
author: fenpho//网站作者
language: zh-CN//语言
timezone://时区

# URL
and root as '/child/'
url: https://fenpho.github.io/ //网站链接
root: /  //网站根目录
permalink: :year/:month/:day/:title/ //时间格式
```
具体的修改方法可以参考官网：[Hexo](https://hexo.io/zh-cn/docs/configuration.html)
### 4、本地预览
1. 生成静态文件
`$ hexo generate  //也可以使用缩写 : $ hexo g`
2. 启动服务器
默认情况下，访问网址为：http://localhost:4000/。
`$ hexo server`
运行网上面的命令后，打开浏览器输入http://localhost:4000/即可看到页面了，有木有很激动
### 5、选取主题
接下来你需要做进一步的网站美化工作，到[官网](https://hexo.io/themes/)去选取一个喜欢的主题吧！我采用了一个叫做[TKL](https://github.com/SuperKieran/TKL)的主题：
![我的博客截图](1.png)
确定需要使用的主体之后，打开主题的官网下载安装主题即可：
1. 右键点击根目录，选择git bash
![](2.png)
2. 运行如下命令（去主题的github页面找类似下面的命令）
`$ git clone https://github.com/SuperKieran/TKL.git themes/tkl`
命令中的后面的tkl为存储的目录名字，可以随便修改
3. 更新主题相关文件
```
cd themes/cafe
git pull
```
4. 使用主题
修改根目录下的博客配置文件 `_config.yml` 主题属性 theme 为 `cafe`.
5. 配置主题，这个需要根据不同主题的说明来配置，也可以不配置

好了，主题安装好了，此时需要使用如下命令：
```
hexo clean && hexo g
hexo server
```
完成后刷新页面看一下吧
### 7、添加文章
创建一条博文，运行下面的命令，或者直接新建一个Markdown文件，非命令行新建文件需要手动添加文章头部（注意目录source/_posts）
 `hexo new "your-post-name"`
如果想要在新建的同时生成对应的文件夹，用于存放文档的资源文件，如图片，音视频等：将配置文件中的post_asset_folder的值从false改为true即可
`post_asset_folder: true`
### 8、文章分类
1. 在根目录下scaffolds/post.md中，添加一行categories:（同理可应用在page.md和photo.md）
```
---
title: {{ title }}
date: {{ date }}
categories:
---
```
2. 在文章的开头配置
```
---
layout: post
title: 标题
date: 2017-05-26 09:00
author: "Fenpho"
categories:
	- 目录名字 
tags:
	- 标签1
	- 标签2
---
```
3. 第三步：配置博客首页归档展示样式。修改主题的配置文件themes目录下对应的主题下面的_config.yml中: 
```
# 博客首页展示文本/访问路径/自定义归档名称
menu:
  home: /
  essay: /categories/随笔     
  write: /categories/写作     
  about: /about
```
### 9、添加文章置顶功能
原理：在Hexo生成首页HTML时，将top值高的文章排在前面，达到置顶功能。修改Hexo文件夹下的node_modules/hexo-generator-index/lib/generator.js，在生成文章之前进行文章top值排序。
需添加的代码：
```
posts.data = posts.data.sort(function(a, b) {
if(a.top && b.top) { // 两篇文章top都有定义
  if(a.top == b.top) return b.date - a.date; // 若top值一样则按照文章日期降序排
  else return b.top - a.top; // 否则按照top值降序排
}
else if(a.top && !b.top) { 
// 以下是只有一篇文章top有定义，那么将有top的排在前面
  return -1;
}
else if(!a.top && b.top) {
  return 1;
}
else return b.date - a.date; // 都没定义按照文章日期降序排
});
```
其中涉及Javascript的比较函数：
```
cmp(var a, var b) {
return a - b; // 升序，降序的话就 b - a
}
```

修改完成后，只需要在需要置顶的文章上面加上top值，将会根据top值大小来选择置顶顺序top值越大越靠前。需要注意的是，这个文件不是主题的一部分，也不是Git管理的，备份的时候比较容易忽略。
以下是最终的generator.js
```
'use strict';
var pagination = require('hexo-pagination');
module.exports = function(locals){
  var config = this.config;
  var posts = locals.posts;
    posts.data = posts.data.sort(function(a, b) {
        if(a.top && b.top) {
            if(a.top == b.top) return b.date - a.date;
            else return b.top - a.top;
        }
        else if(a.top && !b.top) {
            return -1;
        }
        else if(!a.top && b.top) {
            return 1;
        }
        else return b.date - a.date;
    });
  var paginationDir = config.pagination_dir || 'page';
  return pagination('', posts, {
    perPage: config.index_generator.per_page,
    layout: ['index', 'archive'],
    format: paginationDir + '/%d/',
    data: {
      __index: true
    }
  });
};
```
### 10、部署到GitHub
#### 10.1 在 GitHub 上的操作
1. 新建一个 Repository
在 Repository name 下填写 yourname.github.io,Description (optional) 下填写一些简单的描述（不写也没有关系），如图所示：
![](3.png)

2. 创建成功之后，进入仓库的设置（点击setting）界面如下图所示：
![](4.png)
找到pages选项，选择master branch作为主页
![image.png](5.png)

简单两步 yourname.github.io 这个域名就配置成功了。

### 10.2、本地操作
1. 为 Hexo 安装 Git 插件
安装 hexo-deployer-git，否则会报 ERROR Deployer not found: git 的错误。
`npm install hexo-deployer-git --save`

修改你的 _config.yml 配置文件，在结尾处加上如下内容：
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:fenpho/fenpho.github.io.git
  branch: master
```
注意repo中的地址为你自己新建的仓库的路径
2. 生成静态文件和部署：
`hexo g & d`

最后出现如下提示就代表成功啦！
INFO Deploy done: git
![](6.png)

**the end！**