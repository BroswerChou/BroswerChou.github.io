---
title: git
top: false
cover: false
toc: true
mathjax: true
date: 2025-04-21 20:07:50
password:
summary:
tags:
categories:
    - 教程
---

# 1、配置Git
>git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"

或者使用
>git config --list查看配置信息
### 情况 1：你还没有初始化 Git 仓库
1、打开 VS Code 中的项目文件夹。

2、打开左侧源代码管理面板（Source Control，快捷键 Ctrl+Shift+G）。

3、点击“Initialize Repository”（初始化仓库）。

4、添加远程地址（先在 GitHub 创建一个新仓库，不要勾选 README）：

5、打开终端，执行：
>git remote add origin https://github.com/你的用户名/你的仓库名.git

6、添加、提交并推送代码：
>git add .
git commit -m "初始化提交"
git push -u origin master  # 有时是 main，下面说明

⚠️ 注意：GitHub 默认分支是 main，如果你的本地是 master，第一次推送时可能需要：
>git push -u origin master:main

或你可以改本地分支：
>git branch -M main
git push -u origin main

### 情况 2：你已经初始化并有远程地址
只需要执行情况1的第六步操作

如果推送时间显示不能连接到服务器，请使用ssh连接，执行下面命令：
>git remote set-url origin git@github.com:用户名u/仓库名.git

然后再尝试推送
