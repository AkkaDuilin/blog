---
title: hexo使用指南
tags: 

    - hexo
copyright: true
date: 2021-11-01 17:46:11
permalink:
categories:

    - 博客
description:
image:
---

<img src="https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fwww.zyiz.net%2Fupload%2F202002%2F18%2F202002182223498227.png&refer=http%3A%2F%2Fwww.zyiz.net&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1640944017&t=77d83c28c44b14310d74a639bf7b5d62/" alt="" style="width:100%" />  

**前言**

记录一下hexo搭建博客的操作和一些小知识 


<!-- more -->

#  **常用操作** 


```
    hexo d 上传至github
    hexo new [layout] <title>
    eg: hexo new post name 新建页面
    hexo help  # 查看帮助
    hexo version  #查看Hexo的版本
    hexo algolia  # 更新search庫
    hexo clean #清除部署緩存
    hexo n == hexo new #新建文章
    hexo g == hexo generate #生成静态页面至public目录
    hexo s == hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
    hexo d == hexo deploy #将.deploy目录部署到GitHub
    hexo d -g #生成加部署
    hexo s -g #生成加预览~~
```


# 常用语言用法

```

    代码块
    {% codeblock [xxxxxx] [lang:]  %}{% endcodeblock %}

    图片
    <img src="" alt="" style="width:100%" /> 

    博客内页面跳转
    {% post_link 最小生成树 %}
    {% post_link 最小生成树 最小生成树 %}

    <table>
        <tr>
            <td ><center><img src="" >图1 </center></td>
            <td ><center><img src="" >图2 </center></td>
        </tr>

    </table>

    制表
    |  序号 | 方法 | 描述 |
    |:-----|:-----|:-----| 
    |       |       |       |
```


#  Hexo部署出现错误err: Error: Spawn failed解决方式
1. 
## 进入站点根目录
cd /usr/local/src/hexo/hanyubolg/

## 删除git提交内容文件夹
rm -rf .deploy_git/

## 执行
git config --global core.autocrlf false

## 最后
hexo clean && hexo g && hexo d

2. 
## 进入站点根目录
cd /usr/local/src/hexo/hanyubolg/

## 删除git提交内容文件夹
vim _config.yml

## 修改
deploy:

type: git

repo: https://github.com/yourname/yourname.github.io.git -> git@github.com:a956551943/weixiaohui.github.io.git

branch: master

## 最后
hexo clean && hexo g && hexo d