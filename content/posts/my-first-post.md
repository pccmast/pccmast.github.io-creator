---
title: "My First Post"
date: 2020-09-15T19:50:35+08:00
draft: false
---

# 我的第一篇博客

## 安装Hugo
* Mac 安装方式：

        brew install hugo
        hugo version
    
* Windows 安装方式：
    1. [Hugo release](https://github.com/gohugoio/hugo/releases) 网站下载 hugo
    2. 解压hugo文件夹
    3. 把 ...\hugo 加入PATH
    4. 重启终端

安装完成的标志：命令行输入 `hugo version` 显示代码

## 使用 Hugo+Github 快速搭建博客

### Hugo 生成页面

##### 1. 进入 Hugo 官网，点击首页的 Quick Start， 按照官网教程操作。

##### 2. 命令行操作，新建一个网站。

        hugo new site 网站名
        
* 该命令会在当前目录下新建 `网站名` 文件夹。
* 在这里将文件夹取名`pccmast.github.io-creator`

##### 3. cd 进入新创建的文件夹，使用`git init`，新建仓库, 并从github 下载网站主题

```shell
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
```

把主题添加到网站设置中

```shell
echo 'theme = "ananke"' >> config.toml
```

##### 4. 添加一些内容

```shell
hugo new posts/my-first-post.md
```
文件头： 

       
    ---
    title: "My First Post"
    date: 2019-03-26T08:47:11+01:00
    draft: true
    ---
    
要把 draft 草稿改成 true，这样就可以把这个文件放出来。这个文件是网站的首页。
    
##### 5. 启动服务器
        
        hugo server // 查看非草稿页面
        hugo server -D  // 查看草稿界面
        
    
当前目录位于 `网站名` 的时候，可以输入以上命令（http://localhost:1313/） 进入网页

##### 6. 客制化主题

新建一个 bash，在 bash 中输入`code .` , 找到config.toml, 在 baseURL 中输入你的网站首页，把 languageCode 的值改为"zh-Hans"

##### 7. 生成静态网页

在命令行中输入 `hugo -D` , 生成静态网页。输出会放置于当前的新建文件夹 public 下。public 就是一个网页，但是只能在 hugo 中查看。

### 使用 github pages 查看网页

##### 8. github 创建仓库

在 github 网站生成一个仓库，名字就是你的网页名，`pccmast.github.io`, 创建的时候啥也不要勾选

##### 9. public 关联远程仓库
* 命令行进入 public 文件，使用 `git init ` 创建一个本地仓库。并且 `git add .` 、`git commit -m ...`。
* 然后关联远程仓库, 使用 github 提供的代码。
* 
```shell
git remote add origin git@github.com:...
git push -u origin master
```

##### 10. 在 github 仓库页面点击 settings

找到 github pages 栏目， 点击网址即可进入你的博客网站。