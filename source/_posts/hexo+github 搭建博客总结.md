---
title: hexo+github pages 搭建博客总结
date: 2016-01-20 16:49:44
tags: 
 - Git 
 - Github 
 - Hexo
 - 技术 
 - Markdown
---
## 1.前言

   一直都希望能自己搭建个博客出来，所以在考完试后，也是从网上参考了很多用hexo+github pages搭建博客的文章，折腾了一天多，中间也是出现了一些问题，有一些还是暂时没有解决的问题。

   在搭建之前要对所用到的工具框架有个了解：
   * [Git](http://git-scm.com/book/zh/v2)
   * [Github](https://github.com/)
   * [Github Pages](https://pages.github.com/)
   * [Hexo](https://hexo.io/zh-cn/)
   * [Markdown](http://wowubuntu.com/markdown/basic.html)

此外，在搭建过程中参考的文章有:
1.[hexo你的博客](http://ibruce.info/2013/11/22/hexo-your-blog/)
2.[GitHub-Pages-Hexo搭建博客](http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/)
3.[Hexo系列教程](http://zipperary.com/categories/hexo/)
4.[使用GitHub和Hexo搭建免费静态Blog](http://wsgzao.github.io/post/hexo-guide/#准备工作)

## 2.配置Hexo

   首先查看Hexo的文档了解了Hexo的基本概念以及如何安装，当然还有使用的方法。
  
   Hexo官方文档（https://hexo.io/zh-cn/docs/index.html）

（所以下面会有一大段是摘自官方文档的，当做笔记记录下）

  **Hexo**

   Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页

### (1) 安装前提

安装Hexo的官方文档，需要安装有下面两个应用程序：
* [Node.js](https://nodejs.org/en/)
* [Git](http://git-scm.com/)

**安装Node.js**
我使用的是从[Node.js](https://nodejs.org/en/)上下载安装，另一种安装方法是[nvm](https://github.com/creationix/nvm)

**安装Git**
我是使用官方版本的安装[Git](https://git-scm.com/download/win),当然也是由于我是在win10上配置的，所以会选择这种方式，另外，还有一种安装方式：[GitHub for Windows](https://desktop.github.com/)

如果是linux的话，就直接一行命令搞定了:

(Ubuntu,Debian):    
`sudo apt-get install git-core`

(Fedora,Red Hat,CentOS):    
`sudo yum install git-core`

Mac：使用[Homebrew](http://brew.sh/),[MacPorts](http://www.macports.org/) 或下载 [安装程序](http://sourceforge.net/projects/git-osx-installer/) 安装。

**Git配置以及使用**
有关Git的配置以及如何使用，我初学的时候，是根据[廖雪峰老师的Git教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001373962845513aefd77a99f4145f0a2c7a7ca057e7570000)，这个教程简单易懂，看完是基本能懂得如何使用Git，并且教程还有教如何添加远程仓库，也就是Github，也就是如何关联一个远程仓库。

相关的一些资料：
* [猴子都能懂得GIT入门](http://backlogtool.com/git-guide/cn/intro/intro1_1.html)
* [Git Magic](http://www-cs-students.stanford.edu/~blynn/gitmagic/intl/zh_cn/)
* [Git 资源整理](http://www.jianshu.com/p/25647b9920b7)
* [Github使用（一）生成本地项目上传](http://bach-dream.iteye.com/blog/1325159)
* [Git全解析之用起来先](http://wustrive2008.github.io/2016/01/06/%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6/Git%E5%85%A8%E8%A7%A3%E6%9E%90%E4%B9%8B%E5%85%88%E7%94%A8%E8%B5%B7%E6%9D%A5/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io),这个教程有附带一个关于git的知识结构图,如下所示:

![git image](http://7xifb5.com1.z0.glb.clouddn.com/wustrive-hexogit%E7%9F%A5%E8%AF%86%E7%BB%93%E6%9E%84.png)

**Github**
• 首先要注册一个Github的账号
• 建立一个与用户名对应的仓库，即仓库名为[your_user_name.github.com]或者[your_user.name.github.io]
• 添加SSH公钥到 Account settings -> SSH Keys -> Add SSH Key
关于添加SSH公钥的可以参考以下资料:
[Generating SSH keys](https://help.github.com/articles/generating-ssh-keys/)
[Error: Permission denied (publickey)](https://help.github.com/articles/error-permission-denied-publickey/)


### (2) Hexo的安装和使用

#### 安装

安装上面两个必须的应用程序后，就可以使用npm安装Hexo:
`$ npm install -g hexo-cli `

#### 使用

安装完成后，可以使用如下命令初始化:
`$ hexo init <folder>`
`$ cd <folder>`
`$ npm install`

当然也可以先直接进入需要使用Hexo的文件夹，执行:
`$ hexo init`
`$ npm install`

初始化后的结果，就是在指定文件夹中，目录如下:

    .
    ├── _config.yml
        ├── package.json
    ├── scaffolds
    ├── source
    |   ├── _drafts
    |   └── _posts
    └── themes

其中，source\_posts 文件夹就是存放博客的文章，也就是.md文件

_config.yml是配置文件，主要是对这个文件进行配置，比如博客的名字，菜单显示，使用的主题等

scaffolds文件夹是模板文件夹，新建文章的时候，Hexo会根据它来建立文件

themes文件夹就是主题文件，Hexo会根据主题来生成静态页面，在Hexo中可以使用的主题是有很多的，可以从[Themes](https://github.com/hexojs/hexo/wiki/Themes)上选择自己喜欢的主题，更换主题需要将根目录下的**_config.yml**文件中的`theme:Landscape`更改成`theme:your_theme`,其中，**Landscape**是默认的主题

**本地浏览**
在执行下列命令后，就可以在浏览器中输入`localhost:4000`进行本地的浏览：

    $ hexo generate
    $ hexo server

**但是在这步，我是一直都不成功，无论是输入`localhost:4000`,`127.0.0.1:4000`,这个问题我是百度了很久，发现在hexo的github的issue有人有同样的问题--[win10系统hexo s以后http://localhost:4000打不开本地服务器 #1568](https://github.com/hexojs/hexo/issues/1568)，现在这个问题我也是还没有搞明白为什么。**

虽然无法本地浏览，但是这也不是什么大问题，最终还是要部署在Github Pages上的

### (3) 部署到Github

在部署到GitHub前，需要安装一个插件:
`$ npm install hexo-deployer-git --save`
然后就修改根目录下的_config.yml文件中的:

    # Deployment
    ## Docs: https://hexo.io/docs/deployment.html
    deploy:
    type:

修改后的结果是：

    deploy:
     type: git
     repo: git@github.com:ccc013/ccc013.github.io.git
     branch: master
**repo**是填写对应仓库的SSH地址
然后执行下列命令即可：

    $ hexo generate
    $ hexo deploy
或者是`hexo deploy -g`也是同样的效果，然后就可以在浏览器中输入username.github.io进行浏览

但是这样在Github中的文件就是通过命令`hexo generate`生成的网站文件，而初始化生成的文件还是在本地电脑中的，也就是原始的文章是没有上传到Github的，这样如果更换了机器就不能继续修改你的博客了。

所以是希望在Github上可以保存原来的文章文件，这个方法呢，很多人都是用到的，就是在Github上建立分支了，比如建立一个hexo分支，然后设置它为默认分支，设置方法在**Settings->Branches**中

这个过程我初始是按照[GitHub-Pages-Hexo搭建博客](http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/)中来做的，但是在输入`hexo init`后，就会发现一开始`git clone`下来的文件中的.git文件没有了，并且之后也是无法`git push `到自己的github上，总是显示被拒绝的提示，本来我都是打算再建立一个仓库来存放文章了，但是后来又在上网搜索，看到这篇文章[如何使用Hexo在Github上搭建自己的博客](http://www.xrpmoon.com/blog/archives/jripple1281.html)中发布到github page的时候，就想自己应该是在本地的时候也是要新建一个同样名为hexo的分支，然后`git commit`到这个分支，于是就这么做，没想到真的成功了！

### (4) 博客管理流程
所以现在对博客的修改就是如同[GitHub-Pages-Hexo搭建博客](http://crazymilk.github.io/2015/12/28/GitHub-Pages-Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/)中说得一样:
**日常修改**
1. 在本地修改博客，如添加新的博文，修改样式等；
2. 在hexo分支下，依次执行`git add .`,`git commit -m "..."`,`git push origin hexo`,将改动push到GitHub上；
3. 再执行`hexo deploy -g`,发布网站到master分支上。

**更换电脑或者本地资料丢失**
1.使用 `git clone git@github.com:ccc013/ccc013.github.io.git` 拷贝仓库；
2.在本地拷贝下来的ccc013.github.io文件夹中通过Git bash依次执行下列命令：
    
    npm install hexo
    npm install
    npm install hexo-deployer-git
这里就不需要`hexo init`这个命令

### (5) 使用问题总结
1. /c/Users/cai/AppData/Roaming/npm/hexo: line 12: node: command not found
(更新于2016-03-07)

在搭建完博客后，有一段时间没有使用后，然后需要更新下博文或者样式时，在Git bash敲下命令`hexo g`，居然出现上述错误信息，然后发现输入任何有关hexo的命令都是同样的错误，我又试着敲了npm这个命令，发现也是出错的，但是在系统命令行中输入`node -v`和`npm -v`,都正常显示了版本信息，于是我想估计是环境变量设置有问题，我在用户的环境变量PATH中添加了两个路径，分别是`C:\Users\cai\node_modules\hexo\bin`和`C:\Program Files\nodejs`，再加上原来就添加的路径`C:\Users\cai\AppData\Roaming\npm`，发现就解决这个问题了，可以正常修改博文，然后发布网站。

不过，我也不清楚是否完全解决这个问题，还需要观察一段时间。

### (6) Markdown知识点总结

**生成md文件**
命令`hexo new "文件名"`就可以生成一个md文件，然后就可以开始写文章，但是这里用到Markdown的语法，同时我们也需要一个专门可以用来写markdown的工具。

这个工具，我使用的是[sublime text 3](http://www.sublimetext.com/3),这是一个文本编辑器，可以支持多种编程语言和文件格式，当然也就包括Markdown语法，具体配置方法可以参考如下:
[Sublime Text 全程指南](http://zh.lucida.me/blog/sublime-text-complete-guide/),
[Sublilme Text 资源整理](https://github.com/jikeytang/sublime-text)
[Sublime进阶使用](http://blog.saymagic.cn/2015/06/20/write-blog-by-sublime.html)

这个工具还是非常强大的，之前是我用来写python的，现在搭建博客后，就可以用来写Markdown的文件了。

**Markdown语法**
具体的可以参考[Markdown 语法说明](http://wowubuntu.com/markdown/index.html#code)

这里就记录下暂时用得比较多的：

**标题**
`=`,`-` 分别表示最高阶和第二阶标题，这两种是在文字下一行插入；

在行首插入1到6个`#` 分别对应标题1到6

**段落和换行**
一个 Markdown 段落是由一个或多个连续的文本行组成，它的前后要有一个以上的空行（空行的定义是显示上看起来像是空的，便会被视为空行。比方说，若某一行只包含空格和制表符，则该行也会被视为空行）。普通段落不该用空格或制表符来缩进。

**列表**
无序列表使用星号、加号或者减号，而有序列表是数字加一个英文句点`.` 

**代码和代码区块**
使用一个反引号``可以得到代码，而代码区块是每行缩进4个空格或者一个制表符，也就是键盘上的Tab键，当然首先跟上一行要隔着一个空行才行。

* * * 

**分隔线**
在一行中使用三个以上的星号、减号、底线来建立一个分隔线，行中不能有其他东西。

**链接**
用的比较多的是行内式，也就是一个方括号`[]`后面加一个括号`()`,括号中是链接地址，而方括号中可以是网址的标题，或者对你对网址内容的简单总结

**强调**
一个`*`或者`_`包围的文字是斜体的效果，而两个`*`或者`_`包围则是强调的效果

**图片**
格式如下：

    ![image](/path/img.jpg)
    ![image](/path/img.jpg "title")
方括号中是图片的替代文字，而第二种写法中最后的引号内容是可以选择的标题文字

**锚的使用**
使用命名锚，我们就可以创建目录，点击目录就可以跳至该命名锚，也就是同一个页面中某个小节的位置。

一开始是根据markdown的语法，但是发现并没有实现这个功能，后来搜索了下，根据[markdown中命名锚](http://ju.outofmemory.cn/entry/115045)中给出的方法，也就是使用html的语法，也就是目录使用，比如`[Overview](#overview)`,而在命名锚所要到的位置，使用如`<h3 id="overview">Overview</h3>`,主要是**id**属性来命名锚，这样点击目录中的Overview,就会跳至`<h3 id="overview">Overview</h3>`处了。

## 3 总结

从昨天，也就是1月20号弄了一天，但是并没有解决如何在Github上存放原始文章文件，今天下午则是找到解决方法，并且成功解决了，然后写下这篇总结。

目前完成的也只是比较简单的内容，还有很多内容可以增加，此外搭建这个博客的本意是促使自己可以多总结多写博客，最终的目的是要掌握好学到的技术知识，所以现在仅仅是一个准备动作，最多也就是迈出一小步了，还需要自己不断坚持，不断学习，不断努力！
   