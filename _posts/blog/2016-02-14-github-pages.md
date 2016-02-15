---
layout: post
title: 使用Github Pages建独立博客
description: Github本身就是不错的代码社区，他也提供了一些其他的服务，比如Github Pages，使用它可以很方便的建立自己的独立博客，并且免费。
category: blog
---

今天是个普天同庆的好日子，2月14情人节，然而作为单身狗，这一切跟我并没有关系……并且，由于我昨天一时冲动，决定从今天开始写毕业论文（好吧其实并不是我自己主动决定的，毕竟deadline才是第一生产力……已经不写不行啦）。

上面一堆都是废话，我真正想说的是，晚上花了一个多小时终于搭好了自己的github page(不要说我身为程序员为啥连这个都不会，毕竟我是个弱鸡……)。网上找了好多教程，动不动就是洋洋洒洒一大堆，好高端耶~看的我头昏眼花，然而我只是想搭一个纯粹的github page，我连自己的域名都不想买好吗，没错我就是这么懒。

于是为了庆祝我的github page搭建成功，也为了总结经验，我决定写一篇最简单的github page搭建攻略。

我参考的主要是[BeiYuu.com](http://beiyuu.com)的[使用Github Pages建独立博客](http://beiyuu.com/github-pages/)，因为不打算购买域名，所以跳过独立域名的部分。

## 配置和使用Github
身为一只程序员，git的使用的基本技能，此处略过。

## 使用GitHub Pages建立博客
因为BeiYuu的文章太长而且并不详细，所以建立github page时我参考的是[这里](http://www.cnblogs.com/purediy/archive/2013/03/07/2948892.html)。

主要步骤就是

1. 建立一个名为xxx.github.io的repo，这里的xxx是你的github帐号名。

2. 进入这个仓库，选择settings，在Update site下选择一个主题（适合懒人），当然你愿意自己写主题也没问题……
![图片来源于http://www.cnblogs.com/purediy/archive/2013/03/07/2948892.html，侵删](http://images.cnitblog.com/blog/275810/201303/07214412-d3e051f728a4498d8ea7841a04b48f38.png)

3. 引入jekyll管理静态模板。也就是复制一个jekyll的项目到我们刚刚的项目文件夹下面。我用的是[Beiyuu的][11]

4. 更改配置文件。首先是CNAME，因为我木有自己的域名，所以把CNAME底下的域名就改成github page的域名（即xxx.github.io）。其次是config.ynl文件，把里面的markdown版本改为kramdown，因为原来的项目是12年的，现在已经不用它当时所使用的Markdown引擎了。还有title,author_info,url也改一改，毕竟谁都不想自己的博客还挂着别人的名字吧。
至于其他的就没太大必要改了，想改就改，不改也没影响。

话说beiyuu这个样式，所有外链都有个小图标，鼠标Hover变成红色，还是挺别出心裁的。看了一下，是通过Js给a标签加了个类external实现的。


## Jekyll模板系统

下面都是从Beiyuu那篇文章里抄的。

> GitHub Pages为了提供对HTML内容的支持，选择了[Jekyll][]作为模板系统，Jekyll是一个强大的静态模板系统，作为个人博客使用，基本上可以满足要求，也能保持管理的方便，你可以查看[Jekyll官方文档][8]。

你可以直接fork[我的项目][11]，然后改名，就有了你自己的满足Jekyll要求的文档了，当然你也可以按照下面的介绍自己创建。

### Jekyll基本结构
**Jekyll的核心其实就是一个文本的转换引擎**，用你最喜欢的标记语言写文档，可以是Markdown、Textile或者HTML等等，再通过`layout`将文档拼装起来，根据你设置的URL规则来展现，这些都是通过严格的配置文件来定义，最终的产出就是web页面。

基本的Jekyll结构如下：

    |-- _config.yml
    |-- _includes
    |-- _layouts
    |   |-- default.html
    |   `-- post.html
    |-- _posts
    |   |-- 2007-10-29-why-every-programmer-should-play-nethack.textile
    |   `-- 2009-04-26-barcamp-boston-4-roundup.textile
    |-- _site
    `-- index.html


简单介绍一下他们的作用：
#### _config.yml
配置文件，用来定义你想要的效果，设置之后就不用关心了。

#### _includes
可以用来存放一些小的可复用的模块，方便通过`{ % include file.ext %}`（去掉前两个{中或者{与%中的空格，下同）灵活的调用。这条命令会调用_includes/file.ext文件。

#### _layouts
这是模板文件存放的位置。模板需要通过[YAML front matter][9]来定义，后面会讲到，`{ { content }}`标记用来将数据插入到这些模板中来。

#### _posts
你的动态内容，一般来说就是你的博客正文存放的文件夹。他的命名有严格的规定，必须是`2012-02-22-artical-title.MARKUP`这样的形式，MARKUP是你所使用标记语言的文件后缀名，根据_config.yml中设定的链接规则，可以根据你的文件名灵活调整，文章的日期和标记语言后缀与文章的标题的独立的。

#### _site
这个是Jekyll生成的最终的文档，不用去关心。最好把他放在你的`.gitignore`文件中忽略它。

#### 其他文件夹
你可以创建任何的文件夹，在根目录下面也可以创建任何文件，假设你创建了`project`文件夹，下面有一个`github-pages.md`的文件，那么你就可以通过`yoursite.com/project/github-pages`访问的到，如果你是使用一级域名的话。文件后缀可以是`.html`或者`markdown`或者`textile`。这里还有很多的例子：[https://github.com/mojombo/jekyll/wiki/Sites](https://github.com/mojombo/jekyll/wiki/Sites)

### Jekyll的配置
Jekyll的配置写在_config.yml文件中，可配置项有很多，我们不去一一追究了，很多配置虽有用但是一般不需要去关心，[官方配置文档][10]有很详细的说明，确实需要了可以去这里查，我们主要说两个比较重要的东西，一个是`Permalink`，还有就是自定义项。

`Permalink`项用来定义你最终的文章链接是什么形式，他有下面几个变量：

* `year` 文件名中的年份
* `month` 文件名中的月份
* `day` 文件名中的日期
* `title` 文件名中的文章标题
* `categories` 文章的分类，如果文章没有分类，会忽略
* `i-month` 文件名中的除去前缀0的月份
* `i-day` 文件名中的除去前缀0的日期

看看最终的配置效果：

* `permalink: pretty` /2009/04/29/slap-chop/index.html
* `permalink: /:month-:day-:year/:title.html` /04-29-2009/slap-chop.html
* `permalink: /blog/:year/:month/:day/:title` /blog/2009/04/29/slap-chop/index.html

我使用的是：

* `permalink: /:title` /github-pages

自定义项的内容，例如我们定义了`title:BeiYuu的博客`这样一项，那么你就可以在文章中使用`{ { site.title }}`来引用这个变量了，非常方便定义些全局变量。

### YAML Front Matter和模板变量
对于使用YAML定义格式的文章，Jekyll会特别对待，他的格式要求比较严格，必须是这样的形式：

    ---
    layout: post
    title: Blogging Like a Hacker
    ---

前后的`---`不能省略，在这之间，你可以定一些你需要的变量，layout就是调用`_layouts`下面的某一个模板，他还有一些其他的变量可以使用：

* `permalink` 你可以对某一篇文章使用通用设置之外的永久链接
* `published` 可以单独设置某一篇文章是否需要发布
* `category` 设置文章的分类
* `tags` 设置文章的tag

上面的`title`就是自定义的内容，你也可以设置其他的内容，在文章中可以通过`{ { page.title }}`这样的形式调用。

模板变量，我们之前也涉及了不少了，还有其他需要的变量，可以参考官方的文档：[https://github.com/mojombo/jekyll/wiki/template-data](https://github.com/mojombo/jekyll/wiki/template-data "Jekyll Template Data")


## 结语

简单的搭建github page就是这样了，至于替换域名，还是等我以后买了域名再说吧……


[BeiYuu]:    http://beiyuu.com  "BeiYuu"
[Github]:   http://github.com "Github"
[jQuery]:   https://github.com/jquery/jquery "jQuery@github"
[Twitter]:  https://github.com/twitter/bootstrap "Twitter@github"
[Github Pages]: http://pages.github.com/ "Github Pages"
[Godaddy]:  http://www.godaddy.com/ "Godaddy"
[Jekyll]:   https://github.com/mojombo/jekyll "Jekyll"
[DNSPod]:   https://www.dnspod.cn/ "DNSPod"
[Disqus]: http://disqus.com/
[多说]: http://duoshuo.com/
[1]:    {{ page.url}}  ({{ page.title }})
[2]: http://markdown.tw/    "Markdown语法"
[3]:    http://baike.baidu.com/view/65575.htm "A记录"
[4]: http://progit.org/book/zh/ "Pro Git中文版"
[5]: http://help.github.com/mac-set-up-git/ "Mac下Git安装"
[6]: http://help.github.com/ssh-key-passphrases/
[7]: http://beiyuu.github.com
[8]: https://github.com/mojombo/jekyll/blob/master/README.textile
[9]: https://github.com/mojombo/jekyll/wiki/YAML-Front-Matter
[10]: https://github.com/mojombo/jekyll/wiki/configuration
[11]: https://github.com/beiyuu/beiyuu.github.com
[12]: http://docs.disqus.com/developers/universal/
[13]: http://mihai.bazon.net/projects/javascript-syntax-highlighting-engine
[14]: http://code.google.com/p/google-code-prettify/
[15]: https://github.com/mojombo/jekyll/wiki/Install
[16]: https://rvm.io/rvm/install/
[17]: http://jekyllbootstrap.com/
[18]: http://chxt6896.github.com/blog/2012/02/13/blog-jekyll-native.html
[a-record]: https://help.github.com/articles/my-custom-domain-isn-t-working
