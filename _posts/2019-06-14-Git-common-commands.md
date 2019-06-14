---
layout: post
title: 'git常用命令'
tags: [code]
---






### 在本地目录下关联远程repository
```shell
git remote add origin git@github.com:git_username/repository_name.git
```

### 取消本地目录下关联的远程库
```shell
git remote remove origin
```


### 在远程仓库创建分支
```shell
git branch 分支名
```
 
### 推送到远程分支
```shell
git push origin 分支名
```

### 取消文件跟踪
```shell
git rm -r –cached 文件
```

### 克隆远程指定分支
```shell
git clone -b v2.8.1 https://git.oschina.net/oschina/android-app.git
```

### 只对github.com代理
```shell
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080
```

### 取消代理
```shell
git config --global --unset http.https://github.com.proxy
```

