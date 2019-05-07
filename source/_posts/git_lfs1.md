---
title: git lfs入门
date:  2019-05-07 12:00:00
tags: [git lfs]
categories: 张永枫
description: gif lfs入门
---

## 适用于大文件版本管理的开源 Git 插件

[添加完成了，可以提交大文件进行测试下](###添加完成了，可以提交大文件进行测试下)

在远程 Git 服务器上存储大文件（例如音频样本、视频、数据集、图形文件等）时，Git 大文件存储（LFS）会将文件内容替换成文本指针储存在 Git 中。

## mac安装

Homebrew : 
```
 brew install git-lfs
```

MacPorts

```
 port install git-lfs
```

## lfs 的使用

### 下载并且安装Git命令插件，只需要进行一次Git LFS 的安装操作。

```
git lfs install
```

### 选择你希望的Git LFS 管理的文件扩展类型（或者直接编辑.gitattributes文件）

```
git lfs track "*.zip"
```

确保.gitattributes 是被追踪的。

```
 git add .gitattributes
```

### 添加完成了，可以提交大文件进行测试下

```
git add file.zip
git commit -m 'add big file'
git push origin master
```

---

The End 

---