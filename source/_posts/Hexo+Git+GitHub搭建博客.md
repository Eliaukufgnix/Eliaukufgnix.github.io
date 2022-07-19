---
title: Hexo+GitHub搭建博客
tags: Git node.js hexo
categories: 博客
top: 1
---

注册GitHub账户并创建远程仓库；安装git和Node.js；使用git bash和npm下载hexo；使用hexo本地编辑博客并实现本地预览；使用git bash部署到GitHub供人浏览观看；主题美化。

<!--more-->

# 主要工具简介

1. **GitHub。**
   使用GitHub托管代码，将你的博客发布到网上供他人浏览。
2. **git(主要使用git bash)。**git–程序员的时光机，保存文件，为你随时恢复你想要的版本。
   本次搭建博客过程中使用git进行版本控制，并将本地仓库托管到GitHub进行管理。
3. **Node.js(主要使用其工具npm下载hexo)。**Node.js 就是运行在服务端的 JavaScript，Node.js 的包管理器 [npm](https://www.npmjs.com/)，是全球最大的开源库生态系统。
   npm相当于软件管家，搜索、下载和删除包。
4. **hexo。**Hexo是一个基于nodejs 的静态博客网站生成器。

# 一、Git

## 1. 下载安装

前往[Git网址](http://gitforwindows.org/)下载安装git即可。
下载安装完成后点击【开始】即可看到

![gitmenu.png](https://img-blog.csdnimg.cn/img_convert/2df50a628d7c6da3ae16dbd1defacfc6.png)

Git CMD：
　　cmd就是添加了一些新功能后的PowerShell。
Git GUI：
　　Git GUI是Git Bash的替代品，为Windows用户提供了更简便易懂的图形界面。
Git Bash：
　　Git中的Bash是基于CMD的，在CMD的基础上增添一些新的命令与功能。所以建议在使用的时候，用Bash更加方便。

## 2. 设置用户

下载后打开Git Bash**第一件事就是设置用户**。目的时告诉远程仓库谁上传的。

```bash
git config --global user.name "GitHub的用户名"（注意前边是“--global”，有两个横线）
git config --global user.email "注册GitHub使用的邮箱"
```

![image-20210618213930953.png](https://img-blog.csdnimg.cn/img_convert/155f93584934706f54729cbde72cb306.png)

然后通过下面代码即可查看用户信息配置。

```bash
git config --global --list
```

## 3. git的简单使用(了解学习)

### 3.1文件上传

```
git add -A //提交所有变化
git commit -m "注释" //添加注释
git push -u 远程仓库的别名(origin) 分支名(master) //上传（-u只在第一次上传时使用即可）
```

### 3.2文件下拉

手动在GitHub网页进行更改后，再次git push会报错，因为本地仓库与远程仓库出现了差异。这时可将远程仓库下拉进行操作。
方法1：`git pull 远程仓库的别名`
方法2:

```
git fetch
git merge
```

**我们可以认为 pull = fetch+merge。git fetch 并没更改本地仓库的代码，只是拉取了远程数据，git merge才执行合并数据。**

**小结**：

**push到远程:**

git add添加到上传缓存区
git commit给缓存区的内容添加备注，此时本地的commit修改啦，但是远程的commit和文件都没修改。
git push 修改远程文件和commit信息
**下拉文件**：

git fetch 将数据拉下来，但是没修改本地的commit和文件
git merge 改变本地数据

### 3.3文件克隆

使用的命令为：

```
git clone 链接地址
```

打开GitHub仓库点击右上角的绿色按钮Code

![img](https://img-blog.csdnimg.cn/img_convert/00b40803fa6b9077034c6205102a0d81.png)

其中链接地址有三种：

1.https 均可使用

2.SSH 仓库主人是你

3.GitHub CLI 新出的GitHub命令行模式

还有两种Open with Github Desktop（在桌面版GitHub打开）和Download zip（下载压缩文件）

**区分一下zip和git clone：**

1.采用git clone的项目包含.git目录，这里面有历史版本信息

2.采用下载zip文件的是没有版本历史信息的。只是当前分支的最新版本

## 4. git进阶

### 4.1、工作机制

![image-20220718234432470](C:\Users\F\AppData\Roaming\Typora\typora-user-images\image-20220718234432470.png)

### 4.2、配置git

| 命令名称                             | 作用              |
| ------------------------------------ | ----------------- |
| git config --global user.name 用户名 | 设置用户签名      |
| git config --global user.email 邮箱  | 设置用户邮箱      |
| git config --list                    | 查看git的配置列表 |

### 4.3、git操作


|             命令名称              |                             作用                             |
| :-------------------------------: | :----------------------------------------------------------: |
|             git init              |                         初始化本地库                         |
|          git add 文件名           |                     添加指定文件到暂存区                     |
|             git add .             |               添加该文件夹下的全部文件到暂存区               |
|            git status             | 查看本地库状态<br />初始为空，加入暂存区后为绿色，工作区中添加修改删除文件为红色，提交到本地库时为空。 |
|      git rm --cached 文件名       |                删除暂存区文件。本地文件还在。                |
| git commit -m "日志信息" (文件名) |                         提交到本地库                         |
|            git reflog             |                         查看历史记录                         |
|              git log              |                   查看版本信息（更为详细）                   |
|      git reset --hard 版本号      |                           版本穿梭                           |

==Git首次安装必须设置一下用户签名，否则无法提交代码。==

注意：这里设置用户签名和将来登录 GitHub（或其他代码托管中心）的账号没有任何关系。

### 4.4、分支的操作

|          命令名称           |             作用             |
| :-------------------------: | :--------------------------: |
|      git branch 分支名      |           创建分支           |
| git branch -m 旧名字 新名字 |          重命名分支          |
|        git branch -v        |           查看分支           |
|     git checkout 分支名     |           切换分支           |
|      git merge 分支名       | 把指定的分支合并到当前分支上 |

#### 4.4.1、合并分支

基本语法：git merge 分支名

①正常合并不冲突
②合并产生冲突

冲突产生的原因：

- 合并分支时，两个分支在同一个文件的同一个位置有两套完全不同的修改。
- 有两套完全不同的修改。 Git无法替我们决定使用哪一个。必须人为决定新代码内容。

解决冲突：

- 编辑有冲突的文件，删除特殊符号，决定要使用的内容
  - 特殊符号：<<<<<< HEAD 当前分支的代码 ==== 合并过来的代码 >>>>>>>hot-fix

- 删除完成之后保存，再次添加到暂存区，并再次提交到本地库
- ==注意：此时使用 git commit 命令时候不能带文件名==

### 4.5、远程仓库操作

|              命令名称              |                           作用                           |
| :--------------------------------: | :------------------------------------------------------: |
|           git remote -v            |                 查看当前所有远程地址别名                 |
|    git remote add 别名 远程地址    |                          起别名                          |
|         git push 别名 分支         |              推送本地分支上的内容克隆到本地              |
|         git clone 远程地址         |                将远程仓库的内容克隆到本地                |
| git pull 远程库地址别名 远程分支名 | 将远程仓库对于分支最新内容拉下来后与当前本地分支直接合并 |

### 4.6、SSH免密登录

1.输入以下命令后，连续按回车键，生成密钥文件。

```bash
ssh-keygen -t rsa -C 自己的邮箱签名
```

2.C:\Users\F\.ssh文件夹下生成文件。

3.复制id_rsa.pub文件中的内容。在github中添加公钥，即可免密登录。

------

参考：[GitHub教程 Git Bash详细教程](https://lolitasian.blog.csdn.net/article/details/79085301)

------

# 二、Node.js

## 1. Node.js和npm简单介绍

Node.js(主要使用其工具npm下载hexo)。Node.js 就是运行在服务端的 JavaScript，Node.js 的包管理器 [npm](https://www.npmjs.com/)，是全球最大的开源库生态系统。相当于软件管家，搜索、下载和删除包。

npm和maven、gradle十分相似。但是maven与gradle是用来管理Java jar包的，而npm是用来管理js的

## 2. Node.js安装

### 2.1 下载

Node.js中文官网：https://nodejs.org/zh-cn/

直接选择下一步完成安装

cmd命令打开使用以下命令查看nodejs版本：

![image-20220219124109050](https://img-blog.csdnimg.cn/img_convert/0f589e6540da9177d8bd1d90e8e2ae3e.png)

安装的文件夹【D:\Environment\nodejs】下创建两个文件夹【node_global】及【node_cache】

![image-20220219124135484](https://img-blog.csdnimg.cn/img_convert/cc22afb64f0bdf3a4d19ff1beebcd2fa.png)

创建完两个空文件夹之后，打开cmd命令窗口，输入

```bash
npm config set prefix "D:\Environment\nodejs\node_global"  //设置使用npm全局安装时下载文件的位置
npm config set cache "D:\Environment\nodejs\node_cache"    //设置缓存位置
npm config set registry https://registry.npm.taobao.org/   //更换镜像源，加快下载速度
npm config list                                            //显示配置信息
```

### 2.2 配置环境变量

==在【系统变量】下新建【NODE_PATH】，输入【D:\Environment\nodejs\node_global\node_modules】==设置下载位置

使用 npm -g 安装的时候，默认的模块D:\Environment\nodejs\node_modules 目录将会改变为

D:\Environment\nodejs\node_global\node_modules目录

==将【系统变量】下的【Path】添加【D:\Environment\nodejs\node_global】==

否则报错：‘vue’不是内部或外部命令，也不是可运行的程序或批处理文件。

### 2.3 安装vue-cli并测试

全局安装hexo

```bash
npm install -g @vue/cli    //全局下载安装vue脚手架
vue -V                    //查看vue版本信息
```

![image-20220221180759907](https://img-blog.csdnimg.cn/img_convert/82aff222f9c8f492180f86ab9a592502.png)

## 3.nvm工具使用

为了方便在不同版本node.js中来会切换，可以使用nvm工具。

参考文章：https://blog.csdn.net/qq_38970408/article/details/124474050

# 三、hexo + github 搭建博客详细教程

hexo是一个基于node.js的快速生成静态博客的开源框架，支持Markdown和大多数Octopress插件，一个命令即可部署到GitHub页面，强大的API，可无限扩展，拥有数百个主题和插件。

## 1. 仓库设置

使用git的主要目的时把本地的代码放到远程仓库进行托管。
主要过程为：

### 1.1 **远程仓库**

打开github，右上角点击new repository

![image-20210619131757783.png](https://img-blog.csdnimg.cn/img_convert/8ded55c54683a67fa1efe54e56b0aff9.png)

填写仓库的相关信息

![image-20220123001120823](https://img-blog.csdnimg.cn/img_convert/d8e50e44aa8140c8692bd736f3e41a2d.png)

### 注意：

后续使用hexo d命令上传的只有静态页而不是你本地仓库的全部文件，这里需要介绍一些特殊情况：**例如更换电脑或者不小心删除了文件夹，因此在创建远程仓库时我们选择为一个仓库创建两个分支。**

```
main //仓库默认分支，用来存放我们的静态页面。
hexo //新建分支为我们的本地仓库进行备份防止丢失。
```

#### 分支：

GitHub里可以创建新的仓库用来托管你的代码，但每各项目都创建一个仓库是不明智的。因此便产生了分支，即在同一仓库下建立不同的分支进行管理。

通过git bash运行以下命令，这里命名新分支为hexo

```
git branch “分支名”` //创建新的分支
git branch  		//查看本地分支
git checkout "分支名"//切换其他分支
git branch -d "分支名"//删除分支
```

然后更换hexo分支设置为默认分支，在后续管理过程中我们只需要管理hexo分支即可。

新建hexo分支，加上默认带的main共有两个分支。hexo分支用来存放网站的原始文件，main用来存放生成的静态文件。

![image-20220123001358069](https://img-blog.csdnimg.cn/img_convert/3fe998183c1d97202b2ca4f1d7b06976.png)

在Setting中设置hexo为默认分支。

![image-20220123225237129](https://img-blog.csdnimg.cn/img_convert/8a0f9f249b799b3483b2d24a5e2fb1b8.png)

### 1.2 建立连接

建立SSH连接是为了方便上传文件，不用每次输入GitHub密码

#### 1.2.1配置SSH

随便找个位置使用Git Bush Here

```bash
~/.ssh   //检查电脑上是否有SSH Key
ssh-keygen -t rsa -C "你的邮箱"  //创建SSH Key
~/.ssh  //再次检查，找到创建的SSH文件,用记事本打开id_rsa.pub文件复制保存
```

在github的Settings中创建一个SSH keys，名字随便起，将复制的内容填入保存

![image-20220124230552742](https://img-blog.csdnimg.cn/img_convert/e4d59855d580005cb4507b074e19806e.png)

测试：

```bash
ssh -T git@github.com
```

![image-20220124233729141](https://img-blog.csdnimg.cn/img_convert/6f33d6b0073555dcd654694c46abca55.png)

详情参考[GitHub教程 SSH keys配置]([GitHub教程 SSH keys配置_LolitaSian-CSDN博客](https://blog.csdn.net/qq_36667170/article/details/79094257))

### 1.3 本地仓库

![image-20220124234246921](https://img-blog.csdnimg.cn/img_convert/da2d5bf70ac5433182cb04ddb045e787.png)

任意文件夹下，将远程仓库克隆到本地，.git隐藏文件，表示让git对该文件夹进行版本控制。

```bash
git clone 仓库的地址（使用ssh不用每次都输入密码，https需要输入密码）
hexo init		//hexo初始化文件夹，会生成很多文件（注意：克隆的仓库文件先放其他位置，否则该命令会报错）
npm install hexo-deployer-git --save	//安装，保证hexo -d命令能使用
```

修改_config.yml中的deploy参数（设置将生成的静态文件上传到main分支）

```bash
deploy:
  type: git
  repo: 仓库地址
  branch: main
```

依次执行以下命令提交网站相关的文件（hexo存放网站的原始文件）

```bash
git add .
git commit -m "init"
git push origin hexo
```

### 1.4 更换电脑如何使用

安装Node.js，Git和hexo-cli脚手架

拷贝仓库（默认分支为hexo）

```bash
git clone 仓库的地址
```

在本地新拷贝的http://CrazyMilk.github.io文件夹下通过Git bash依次执行下列指令：

```bash
npm install
npm install hexo-deployer-git --save（记得，不需要hexo init这条指令）
```

## 2.新建文章

### 2.1新建文章

方式一：

```
hexo new "文章名"
```

默认是创建在(E:/blog/source/_posts)下的

方式二：

直接在创建的文件夹下(E:/blog/source/_posts)新建.md文件来编写博客内容。可以新建文件夹对文章进行分类，方便管理。

![img](https://img-blog.csdnimg.cn/img_convert/26c038460ee682593aede77c287223fe.png)

```
hexo generate
```

该命令将文本文件解析成网页。

### 2.3本地预览

```
hexo clean
hexo sercer
```

在浏览器访问[http://localhost:4000](http://localhost:4000)即可查看效果，查看完毕后按Ctrl/) + C停止后台服务。

## 3.部署到github

### 3.4部署

```
hexo clean //清除缓存
hexo g //生成静态页
hexo d //部署到github
```

点右上角的setting，进去之后下拉找到git pages，点击链接即可进入你的博客。



