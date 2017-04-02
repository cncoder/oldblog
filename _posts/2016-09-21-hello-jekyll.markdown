---
layout:     post
title:      "利用GitHub Pages10分钟打造个性域名博客"
subtitle:   " \"只需要买个域名，服务器的钱都省了，0环境要求\""
date:       2016-09-21 00:00:00
author:     "Romennts"
header-img: "img/post-bg-2015.jpg"
tags:
    - Tech
    - 自制教程
---

> “先到github fork 我的blog库即可创建自己的GitHub Pages ”


## 前言

一直觉得wordpress太重了，终于改成Jekyll了，而且jekyll更加注重写作本身。



作为一个程序员， Blog 这种轮子要是挂在大众博客程序上就太没意思了。一是觉得大部分 Blog 服务都太丑，二是觉得不能随便定制不好玩。


<p id = "build"></p>
---

## 正文

接下来说说搭建这个博客的技术细节。  

正好之前就有关注过 [GitHub Pages](https://pages.github.com/) + [Jekyll](http://jekyllrb.com/) 快速 Building Blog 的技术方案，非常轻松时尚。

其优点非常明显：

* **Markdown** 带来的优雅写作体验
* 非常熟悉的 Git workflow ，**Git Commit 即 Blog Post**
* 利用 GitHub Pages 的域名和免费无限空间，不用自己折腾主机
	* 如果需要自定义域名，也只需要简单改改 DNS 加个 CNAME 就好了
* Jekyll 的自定制非常容易，基本就是个模版引擎

---

配置的过程中也没遇到什么坑，基本就是 Git 的流程，相当顺手

大的 Jekyll 主题上直接 fork 了 Clean Blog（这个主题也相当有名，就不多赘述了。唯一的缺点大概就是没有标签支持，于是我给它补上了。）

本地调试环境需要 `gem install jekyll`，结果 rubygem 的源居然被墙了……后来手动改成了我大淘宝的镜像源才成功

Theme 的 CSS 是基于 Bootstrap 定制的，看得不爽的地方直接在 Less 里改就好了（平时更习惯 SCSS 些），**不过其实我一直觉得 Bootstrap 在移动端的体验做得相当一般，比我在淘宝参与的团队 CSS 框架差多了……** 所以为了体验，也补了不少 CSS 进去

最后就进入了耗时反而最长的**做图、写字**阶段，也算是进入了**写博客**的正轨，因为是类似 Hack Day 的方式去搭这个站的，所以折腾折腾着大半夜就过去了。

第二天考虑中文字体的渲染，fork 了 [Type is Beautiful](http://www.typeisbeautiful.com/) 的 `font` CSS，调整了字号，适配了 Win 的渣渲染，中英文混排效果好多了。


##详细教程

### Choose Your Favorite Blog Theme

因为在主题模板方面吃过好多亏了...所以怕麻烦的同学直接fork我的就可以了。具体请探索——

[Microdust博主写的Jekyll 博客主题精选](http://azeril.me/blog/Selected-Collection-of-Jekyll-Themes.html)

可以从中找自己合意的，然后去对应的 GitHub 仓库 Fork/Clone 就行。

每个精选主题，均包括：

* 博客界面截图  
* 创作者个人信息  
* 主题描述  
* 个人评分  
* 可访问的博客站点地址 Live Demo  
* 可直接 Fork 和配置的 GitHub 仓库源码地址。  


### Register GitHub

Jekyll Blog 基于 GitHub 平台，文档存放，后续修改博客设定以及添加博文也都是背靠 GitHub 这座大山。所以首先要拥有一个自己的 GitHub 账号。

注册（免费方案即可） [GitHub](https://github.com/) 并设置个人 ID，在个人的注册邮箱里确认注册，完成登陆。

### Create A Repo

力求快速建站，还是奉行「拿来主义」的策略。在找到合意的 GitHub Pages(这里主要是基于 Jekyll ) 博客主题后，Fork 这个博客主题的 GitHub 仓库。

当然，对于已经下载的博客主题 git 压缩包，可以在网页版主页右上角（ID 头像边），点击「+」，Create New Repository，并通过客户端版将解压的仓库文件上传到该 Repo。或客户端版「Create」选项，创建新仓库并选择该将仓库文件 publish 到 GitHub。

这里有一个**注意点**，无论是 Fork 还是 Create，必须要将这个打算作为博客的 Repo 的标题，命名或改名为如下形式：

> yourname.github.io

yourname 是指你的 GitHub Name，此处命名形式 yourname 必须与你的用户名一致。gh Pages 博客才能生效（ Repo 首次生效需要等待几分钟，生效后就可以访问该博客啦。完成后以后添加或改动的更新都会蛮快同步）。


* Fork a repo;
* Change the repo title to 「yourname.github.io」;
* Waiting for the setting take effect a few nimutes later;
* You can interview the blog from 「yourname.github.io」 on your browser;

## Jekyll Blog Configuration

我们 Fork 的只是别人创造的主题，或者单纯的模板，哪怕生效后访问也没有一点自己的痕迹，那怎么算个人博客呢！接下来就是对博客个性化的过程。

### Jekyll Blog Files Overview

磨刀不误砍柴工。先说明 Jekyll 博客的一般文档类型。

一个典型博客的基础目录结构：

    |-- _config.yml
    |-- index.html
    |-- _includes
    |-- _layouts
    |   |-- default.html
    |   `-- post.html
    |-- css
    |-- js
    |-- _posts
    |   `-- 2015-04-27-Like-Kissing.md
    |-- images
    |   `-- Leah.png
    |-- CNAME
    |-- _404.html
    |-- About.md
    |—— feed.xml
    `-- README.md

### Description of The Catalog Document

目录文档详细说明。如下：    

* _config.yml **博客配置**文档（包括博客标题、favicon、博主 ID、头像、描述、联系方式等基本信息都在这个文档添加或修改）；
* index.html 博客架构文档；
* _includes 博客调用的网页模块（比如导航栏、底栏、博文内容显示、评论模块等），一般不需要管；
* _layouts 存放博客调用的页面模板文件（比如博客主页、具体博文页）的文件夹；
* css 存放博客系统的页面渲染文档文件夹，主要用于调节诸如标题字体、博文字体大小颜色之类；
* js 存放博客调用的 JS 文档文件夹
* _posts **博客正文**存放的文件夹。命名有规定，必须为「日期 + 标题」的模式，即「2015-04-27-Like-Kissing.md」，才能发布到博客里；
* images **图片文件夹**，存放博客相关素材，包括博客 favicon、博主头像等图片及博文贴图素材；
* CNAME 用于绑定个人域名的文档；
* 404.html 「404 Not Found.」站点链接无法访问时的提示页面。
* About.html 博客中的个人说明文档（**About Me**），以 html、md 格式为主；
* feed.xml 博客的 RSS 订阅；
* README.md 项目说明文档。用于 Github 个人项目主页的说明（描述）。

除此之外，还有诸如 fonts 文件夹，存放博客用的字体文件，或有主题是将 css/js/fonts/images 等文件夹合并到 _assets 为名的主文件夹中。404.html/feed.xml/CNAME 文件并非必须，但一般架构完整的博客都有。

### Custom Configuration

自定义修改中，涉及到修改的文档包括：

* _config.yml
* About.html
* CNAME
* images

博客标题、博主 ID 一类都可以直接改。博客 favicon、博主 avatar 一类，还需要到 images 文件夹替换图片和配置文件的对应文件名。注意原图的尺寸，尽量与模板中的原图保持一致。


* [TextMate](https://macromates.com/) / [Sublime Text](http://www.sublimetext.com/) 用于打开 yml/THML 等文件并进行修改。Windows 用户就只有后者可选了...
* [damotou.com](http://www.damotou.com/index.php)  在线制作（转换）用于 favicon（还不知道这是什么？瞧一下自己 Chrome 浏览器书签页左侧的小图标） 的 icon 图片，选择 32*32 像素的图片下载；
* CNAME 文件，如果有独立域名请修改该文件；如果没有，则删掉该文件；如果没有但想要，请看附录。


## Introduction GitHub Desktop

磨刀不误砍柴工，先来了解一下 GitHub 客户端的使用吧。

### Install Git

很多教程谈及 Jekyll 时多半要涉及 Jekyll 本地环境的搭建，但如果不需要频繁预览，并不是必须的。在更新博客的思路上，如果要专业地谈论使用，也多半要挖新坑了——Git 语言的使用。

GitHub 官方推出的 git 客户端，虽然功能简单，但就博客维护的日常提交和同步变动等功能来说，已足够我们使用。

GitHub for Desktop [Windows/Mac](https://desktop.github.com/)  GitHub 的客户端版（区别于命令行工具）。

安装完成后登陆个人账户。立马就开始管理和更新自己的博客啦。

### Login GitHub Account

打开 GitHub 的菜单（切换到 GitHub 界面，Mac 左上角的应用菜单），选择 Preference 偏好选项，点选 Account 登录个人 GitHub 账户。

![GitHubID](http://dreamofbook.qiniudn.com/GithubID.png)

### Clone / Create

Clone 或创建个人博客项目

![GitHub for Mac](http://dreamofbook.qiniudn.com/GithubPic1.png)

在登录后，将已经 Fork 的 GitHub Pages 项目从 GitHub （云端）中， Clone 到本地来，以便于修改。如果已经下载到本地，可以 Create 后将仓库文档拖放进去。

这里再次提醒，gh Pages 项目一般的命名都是「GitHub Name + GitHub.io」形式。不然无法作为个人博客存在。

### Commit & Sync

提交和同步博客的修改

下载完项目后，可以在 Finder 里打开，然后进行查看、修改文档、添加博文之类的操作。

在修改文件（修改文件和添加博文的方法，将在后边说明。）完成后，GitHub 客户端会将文件的修改细节（包括位置和次数）显示出来。由于文件是在本地修改的，因而还需要提交到 GitHub 的服务器上，修改才会最终生效。

![GitHub for Mac2](http://dreamofbook.qiniudn.com/GithubPic2.png)

上图显示的就是提交的流程：

    0. 选择相应的项目（这是是博客项目）；
    1. 如有修改，在 Description 填写说明（可以非常简要，但不能省略）；
    2. 点击「Commit to master」，提交修改；
    3. 点击右上角的「Sync」；
    4. 文件同步完成，片刻后更新生效。

## Introduction Markdown Syntax

好了，前面提了这么多次 Markdown，也该简要介绍一下了。

博文一般都使用 Markdown 语法写作。

Markdown 语法是对纯文本格式的强化，能使文本显示得更清晰、有条理。但它依旧算是简单的文本，很容易修改和扩展，常用于快速写作之中。

Markdown 格式的简洁特性，使之能快速转换为各种互联网上的常用格式，比如 HTML、Word、PDF 等，所以目前越来越常用。

关于 Markdown 语法的细则，请参看 [Markdown 简明语法参考](http://azeril.me/blog/Markdown-Syntax.html)。

嗷，内容太多？但实际用的过程中熟悉起来很快的。花一个小时掌握也差不多啦。


## Create An New Post

接下来我们要开始更新自己的第一篇博文啦。

比较标准的 Jekyll 博客，博文都被放置于 _posts 文件夹中。文档格式为 markdown 或 HTML。当然一般书写 md 文档快捷得多。

如果你打算删除掉这些并非自己所书写的 md 文档（「必须的！」），先熟悉一下这些文件大致的构造再删不迟。

Markdown 文件的命名类型为「日期(20xx-xx-xx) + 主题(英文) + 格式（md/HTML）」。

像这样：

> 2015-04-27-Like-Kissing.md

如果不以这个标准格式命名，文档将无法解析（有的博客也可以，不过标题会默认为文件名，比如我的）。

一般一个 Jekyll 博客，因为主题模板的差异，md 文件也都有些差别。但基本每一篇 Markdown 文档的开头（第一行都为「 ---」）都必须添加一段代码，用以将文档收录到博客以及标签系统中。

所以，一般 md 文档的内容组成都是这样：

* 博文代码
* 正文

### About Markdown File

一个栗子：

例如本博客的文章，代码类型一般是这样：

    ---
    layout: post
    title: 中文简要排版参考
    categories: [blog ]
    tags: [Chinese, Read, ]
    description: 如何创造优美的阅读体验
    ---
    正文开始...

这其中，

* layout 一般不用改；
* Title 一项是必须添加的；
* Categories 目录可以换，但如果不是要多重分类，一般也不用管，这篇归档在 Blog 目录下；
* Tags 可以自己按照文章主题添加，也可以不加，不同的 Tags 直接用英文逗号加半角空格间隔开；
* description 博文概述，一句话概述，一般添加会好些。

有些博客还有博文大图显示、开启或关闭博客评论功能、开启或关闭发布等功能，具体看模板。


所以有必要保存一份在本地，便于发布文章的时候能随时取用。

以下则是（另一个博客主题的模板下）一篇博文内容的栗子：

    ---
    layout: post  
    title: 夏天的烟花（作为标题）  
    description:   
    headline:     
    categories: Blog（作为目录）  
    headline:  
    tags:
      - Photo（添加的第一个标签）
      - Instagram（添加的第二个标签，另起一行）
    comments: ture  
    published: true  
    ---
    正文...

Sample.md 文档后填写相应的内容，开始写博文。Dropbox 文档可以预览时复制粘贴格式到本地的编辑器开始写。

写好文档后将文档保存（修改）为「日期 + 标题」的模式，如：「2015-04-27-Like-Kissing.md」。

然后将 md 文档复制或拖放到 _posts 文件夹里。在 GitHub for Mac 客户端 commit 和 sync，稍等片刻新添加的博文就会自动发布到博客里啦。

## Publish Post With GitHub

如何在网页端在线发布博文？

除了利用 GitHub 客户端以外，还可以通过 GitHub 网站发布博文。这时，如果写作时使用图片，得借助图床，因为网页端无法上传图片。

登录 GitHub gh Pages 博客项目主页。点击主目录中的 _posts 文件夹。然后点击「+」，创建新博文。

![](http://dreamofbook.qiniudn.com/GithubWeb.jpg)

博文结构还是一样：

* 标题
* 博文代码
* 正文

![](http://dreamofbook.qiniudn.com/GithubWeb2.png)

写完后，为本次创建文档的操作输入一段描述，而后确认提交就发布啦。

开始写吧~！

***
✈

## Appendix I 附录 I

### Domain Purchase & Configuration

什么，你还想要为 blog 挑一个更有 feeling 的域名？

GitHub Pages 博客默认关联的是以 yourname.github.io 为格式的网址。如果已拥有自己的个人域名，可以直接在博客的 Repo 主目录里新增一个 CNAME 文件，内容为个人域名。比如，本博客添加的域名记录条目就是「azeril.me」。

什么？还没有，又想要？请继续往下读。

#### Domain

几个比较好的域名服务商：

* [GoDaddy](https://www.godaddy.com/) The World's Largest Domain Name Registrar  
* [Namecheap.com](https://www.namecheap.com/) Cheap Domain Name Registration & Web Hosting  
* [Gandi.net](http://www.gandi.net/) 域名注册商与 VPS Cloud Hosting

绑定到自己的域名

如果是绑定到一级域名：
1. 首先在项目根目录下创建一个叫CNAME文件，里面写上自己的以及一级域名（如这个博客就是skyinlayer.com）
2. 在DNS中为自己的域名增加两条A记录，指向192.30.252.153 和 192.30.252.154
3. 等一会儿（不会超过1小时
4. 如果发生404，baseurl应该为"/"
5. 访问自己的域名看看结果吧


* [官方教程](https://help.github.com/articles/setting-up-an-apex-domain/) Setting up an apex domain 官方说明

如果是绑定到二级域名，需要额外在DNS中增加一条CNAME，指向(github用户名).github.io，然后再CNAME文件中修改为自己的二级域名即可

***
✈

## Reference 参考资料

* [GitHub Pages](https://pages.github.com/) gh Pages 官方说明
* [Jekyll](https://github.com/jekyll/jekyll) GitHub 上的 Jekyll 官方仓库
* [安装 Jekyll](http://jekyllcn.com/docs/installation/) 在本地配置 Jekyll 环境，实现本地 Blog 配置改动和博文发布的预览。
* [使用 Github Pages 建独立博客](http://beiyuu.com/github-pages/)  


## 后记

博主使用过多种方法定义自己的博客，其中就有wordpress ，不是觉得wordpress不好，而是太重，需要挂在挂着mysql。小一点的vps很容易挂掉进程，

最后选择jekyll，毕竟有github 这个靠山。

—— Romennts 重建于2016.9.21
