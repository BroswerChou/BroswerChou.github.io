---
title: pycharm远程连接服务器环境配置
top: false
cover: false
toc: true
mathjax: true
date: 2025-04-09 17:29:43
password:
summary:
tags:
 - 环境配置
categories:
 - 教程
---
#### MobaXterm创建普通用户
切换管理员 sudo -s 
增加新用户 adduser username
输入密码、
查看目录 ls -l /home,出现username目录名即为成功
#### Linux服务器上面安装Anaconda
1、下载anaconda安装包，并将其移入Linux环境中
2、使用chmod +x Anaconda3-2023.09-0-Linux-x86_64.sh命令赋予权限
3、使用./Anaconda3-5.3.0-Linux-x86_64.sh执行安装
4、一直Enter+yes
5、重新打开终端，输入conda -V查看
如果显示does not exit ，请执行chown wj:wj -R /home/wj这条语句，wj改为自己的用户名
#### 配置pytorch
conda create -n 用户名 python=xxx
conda activate 用户名
pip或者conda安装pytorch相关包

#### linux中cuda toolkit安装方法：
1、进入以下网址，选择对应的版本https://developer.nvidia.com
2、执行所给出的命令。如果显示xx不在sudoers文件中，执行下面命令：
	Su root，输入root密码后执行usermod -aG sudo zyt，即可给权限，在安装即可
3、cd /usr/local/cuda-11.8/bin进入文件夹，ls -la查看所有文件，执行./nvcc –version可以查看版本，然后cd ~返回主文件夹
4、sudo nano .bashrc进入编辑，修改路径
5、在最后一行加上 export PATH=/usr/local/cuda-11.8/bin${PATH:+:${PATH}}保存之后重新打开一个终端即可

安装好cuda tookit之后出现新的问题：
NO cuda runtime is found. CUDA_HOME=/usr/local/cuda-11.X
尝试 (1)export FORCE_CUDA=1没用
尝试 (2)export CUDA_HOME=/usr/local/cuda-11.X无用
尝试 (3)切换不同的torch版本进行尝试无用

#### Conda 相关命令
import torch
print(torch.cuda.is_available())  # 是否检测到 CUDA
print(torch.version.cuda)         # 检查 PyTorch 绑定的 CUDA 版本
print(torch.backends.cudnn.version())  # 检查 cuDNN 版本（如果可用）
import torch
print(torch.cuda.is_available())  # 检查是否检测到 CUDA 设备
print(torch.cuda.device_count())  # 检查 GPU 数量
print(torch.cuda.get_device_name(0))  # 获取第一个 GPU 的名称
import torch

print("CUDA available:", torch.cuda.is_available())
print("CUDA version:", torch.version.cuda)
print("cuDNN version:", torch.backends.cudnn.version())
print("GPU device name:", torch.cuda.get_device_name(0))
print("Current GPU:", torch.cuda.current_device())

###### 创建一个张量并移动到 GPU，测试计算是否正常
x = torch.randn(2, 3).cuda()
print("Tensor on GPU:", x.device)
