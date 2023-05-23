---
layout: post
title: 使用github pages创建个人网站
date: 2023-05-23 14:01 +0800
categories: 
- 个人作品
tags: 
- 测试
- 个人网站
---

# 01 前言

首先，本文目的是搭建个人网站，搭建个人网站有很多方法，之前尝试过租用云服务器，使用wordpress搭建，运行了一年时间，没有继续运行下去。主要原因有以下几点：

1. 云服务器是付费的
2. 域名需要购买，并且网站需要备案，流程复杂
3. 使用wordpress搭建的网站上传新文章比较麻烦，不利于频繁更新

所以，当了解到github pages可以解决上述烦恼时，毫不犹豫的选择采用github pages来搭建个人网站。

> **github pages 原理**
>
> 通过Jekyll解析你的github中名为username.github.io的仓库，发布到username.github.io域名上。其中Jekyll 是一个静态网站生成器。它以 Ruby 语言开发，被广泛用于构建静态网站、博客和文档站点。与Jekyll类似的当然还有很多静态网站生成器，这里选择GitHub官方支持的Jekyll。
{: .prompt-tip}


> **警告**
>
> 使用静态网站生成器时，一定不能惯性思维，认为想要修改哪个页面就找到页面的html文件，直接修改，这些网站生成器的特点就是，html等页面是根据配置文件生成的，所以，我们只需要修改配置文件，就能达到修改页面的目的。**Jekyll的配置文件是网站根目录下的_config.yml，当我们需要调整页面时，需要修改这个文件。**
{: .prompt-danger}



# 02 Github Pages 用法
既然是借助github构建个人网站，那么即使我们本地没有任何运行环境也可以。但是如果想在文章发布前在本地进行预览和修改，就需要在本地准备jekyll的运行环境，上面提到了jekyll是ruby语言开发的，所以还需要安装ruby运行环境。
> **友情提示**
>
> 如果想要在本地也能运行网站，会比只使用github pages搭建线上运行的网站多花费几倍甚至十几倍的时间。好处是，在刚开始不熟悉Jekyll时，需要修改页面、文章等来熟悉整个系统的使用，如果没有本地环境，每次修改都上传到github，再由Jekyll自动渲染的话，这个过程非常慢，如果有本地环境，基本上可以做到实时查看修改的效果。
{: .prompt-tip}



## 方案一：不配置本地运行环境

### 1. 选择一个网站主题

从官方主题网站 http://jekyllthemes.org/ 中，选择一个主题，进入主题的github主页

### 2. fork主题

一般如果是个人网站，fork到个人的仓库中时，仓库命名应该为username.github.io

点击项目主页中，项目名称下方菜单栏依次点击settings->pages->Build and deployment，选择master分支，点击保存。等待片刻，就可以访问acsele.github.io了，如果要进行进一步的个性化设置，继续下面的步骤。

### 3. 克隆到本地

在fork后的个人项目username.github.io主页，项目文件列表右上方的code->https，复制项目的github地址，用于本地克隆。

本地打开一个命令行终端窗口，跳转到合适的文件夹，执行git clone "复制的项目https地址"

### 4. 完成readme教程中bundle命令前的步骤
> **友情提示**
>
> bundle命令及其后的内容是在本地搭建网站运行环境，我们不需要本地环境，所以到此为止，后面的工作，当我们把项目push到github的username.github.io仓库后，github会使用Jekyll帮我们完成。
> {: .prompt-tip}

### 5. 提交到github

在项目的根目录下使用Git GUI程序提交，或者依次执行：

```bash
git add .
git commit -m "提交信息"
git push
```

> 不同的主题安装细节不同，而且即使是官方主题网站，很多主题也需要许多额外配置才能达到和项目样例接近，很多主题并不是即开即用，而且，由于在线环境使用github自动部署，因此需要一段时间的延迟，这就导致无法及时发现是因为没有正确配置，还是因为有延迟，导致最终页面效果不理想。因此还是用其他人推荐的主题，或者直接fork其他人的项目，然后添加文章，比较稳妥。
{: .prompt-danger }


## 方案二：配置本地运行环境

> 不同系统的jekyll安装教程地址：https://jekyllrb.com/docs/installation/
{: .prompt-tip }

以下步骤以Windows为例：

### 1. 安装ruby和Jekyll

1. 从[RubyInstaller Downloads](https://rubyinstaller.org/downloads/)下载并安装**Ruby+Devkit**版本。使用默认选项进行安装。
2. 运行`ridk install`安装向导最后阶段的步骤。这是安装带有本机扩展的 gem 所必需的。[您可以在RubyInstaller 文档](https://github.com/oneclick/rubyinstaller2#using-the-installer-on-a-target-system)中找到关于此的更多信息 。从选项中选择`MSYS2 and MINGW development tool chain`。
3. 从开始菜单打开一个新的命令提示符窗口，使对`PATH`环境变量的更改生效。安装 Jekyll 和 Bundler 使用`gem install jekyll bundler`
4. 检查 Jekyll 是否安装正确：`jekyll -v`

### 3. 根据Gemfile安装依赖

在项目根目录下打开命令行窗口，执行`bundle`命令 

### 4. 启动Jekyll网站

项目根目录下打开命令窗口，执行`bundle exec jekyll s`

稍等片刻，项目可以在*[http://127.0.0.1:4000](http://127.0.0.1:4000/)*访问

