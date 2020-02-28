---
title: 抽取 git 仓库的子目录独立成新仓库
date: 2019-11-25 11:37:46
tags: 教程,git
categories: 操作记录

---

## 前言

项目开发中偶尔会碰到这种需求：需要把仓库中的一个子目录独立出来，成为一个全新的独立仓库。但又希望这个新仓库能保留原来所有的提交记录，方面以后查看。

## 操作步骤

### 仓库示例

如下面的目录结构所示，要将项目仓库中 component_a 目录的代码抽取出来，独立成新仓库：

```
- project_root
|- src
|- components
    |- component_a
    |- component_b
```

### 根据子目录新建分支

component_a 目录的提交信息抽出为新的 branch

```
cd {path/to/project_root}
git subtree split -P {component_a 的相对路径} -b {新分支名称}
```

### 新建 component_a 仓库，并从源仓库的新分支中拉内容

```
mkdir ~/component_a
cd ~/component_a
git init
git pull {path/to/project_root} {新分支名称}
```

### 将本地仓库 Push 至远程仓库

上面的步骤操作只是将 component_a 目录独立出来形成了一个本地仓库，还要将该本地仓库 push至远程仓库。

