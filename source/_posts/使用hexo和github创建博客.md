---
title: 使用hexo和github创建博客
top: false
cover: false
toc: true
mathjax: true
date: 2025-04-07 20:58:47
password:
summary:
tags:
categories:
---

# github上面创建仓库
在github上面创建一个新的仓库包含两个分支main和hexo，仓库名称为"用户名.github.io"
main分支用来存储生成的静态网页，进行Github Pages展示；
hexo分支用来存储hexo源码，进行写作和生成网页;

# hexo下载
创建一个新的文件夹用于存储博客信息
打开命令行窗口或者git bash进入到该文件夹下
输如npm i hexo-cli -g安装hexo
安装完成后输入hexo -V验证是否安装成功
输入hexo init初始化文件夹
输入npm install安装相关组件
输入hexo clean清楚冗余文件、输出hexo g生成静态网页、输入hexo s在本地预览

## 1、确保你的 Hexo 项目能正常生成和部署
'''
hexo clean
hexo g
npm install hexo-deployer-git --save
'''
## 2、配置 Hexo 让它把 public/ 推送到 main 分支
'''
deploy:
  type: git
  repo: https://github.com/BroswerChou/BroswerChou.github.io.git
  branch: main
'''
注意repo需要根据使用的是http或者ssh选择不同的链接,branch: main 表示将静态文件推送到 main 分支

## 3、把博客源码推送到 hexo 分支
'''
初始化本地 Git 仓库（如果还没做）:
git init
git remote add origin https://github.com/BroswerChou/BroswerChou.github.io.git

创建 hexo 分支并切换过去：
git checkout -b hexo

把当前 Hexo 项目的源代码（除了 public/）推送到 GitHub 的 hexo 分支:
忽略 public 目录
echo "public/" >> .gitignore

正常提交
git add .
git commit -m "Hexo 源码初始化"
git push origin hexo
'''

## 4、部署博客（生成 + 推送 public 到 main）:
'''
hexo clean
hexo g
hexo d
'''
## 5、启用 GitHub Pages
打开你的仓库、点击右上角 Settings、找到左侧栏的 Pages 或 Pages and Deployment、设置 Source 为：Deploy from a branch → 分支选择 main → 路径保持 / (root)、等几分钟后，访问：👉 https://xxx.github.io

## 部署脚本（一键完成）
可以在根目录下新建一个 deploy.sh 脚本文件（适用于 Git Bash 或 Linux / Mac）：
执行：bash deploy.sh，一键完成源码和部署。
'''
#!/bin/bash
hexo clean
hexo g
hexo d
git add .
git commit -m "更新博客源码"
git push origin hexo
'''
# 写博客文章并发布
1、创建文章：hexo new post "我的第一篇博客"，会在source/_posts/ 目录下创建一个新的 Markdown 文件
2、编写文章：进入.md文档内编写
3、生成静态文件：
'''
hexo clean
hexo g
'''
4、提交文章到Github：
4.1 在hexo分支下面提交博客
'''
确保你在 hexo 分支
git checkout hexo

添加新文件
git add .

提交
git commit -m "添加第一篇博客"

推送到 GitHub
git push origin hexo
'''
4.2 部署到main分支：hexo d
这条命令会将 public/ 文件夹中的静态文件部署到 GitHub 仓库的 main 分支，从而在 GitHub Pages 上展示你的博客。
5、查看博客：https://你的GitHub用户名.github.io



