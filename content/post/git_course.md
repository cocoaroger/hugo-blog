---
title: "Git 使用流程"
date: 2017-09-19T22:23:43+08:00
draft: true
---

#### 生成 ssh key
- 第一个命令，生成密钥：`ssh-keygen -t rsa -C 邮箱地址 -b 4096`, 然后全部回车。
- 第二个命令，拷贝密钥：`pbcopy < ~/.ssh/id_rsa.pub`，

#### 将拷贝好的密钥交个管理员配置权限

#### 克隆项目到本地
- cd 到自己想要放的目录下，如: `cd ~/Desktop`
- 克隆到本地：`git clone git@github.com:cocoaroger/CRTimeButton.git`
