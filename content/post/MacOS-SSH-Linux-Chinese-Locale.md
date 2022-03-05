---
title: "记一次 MacOS SSH Linux 之后出现中文乱码"
date: 2022-01-11T22:44:39+08:00
---

# 一、起因

在开发机器上跑 bazel 构建命令的时候会报错 


```bash
missing input file '//projects/aaa/bbb:public/docs/home/个人中心.md'
```

但是实际上是存在这个文件的。执行 ls 对应目录发现下面的报错

```bash
$ ls xxx/
_sidebar.md  ????????????.md  ????????????.md  ????????????.md  ????????????.md  ????????????.md  ????????????.md
```

比较奇怪，问了其他同学说没有这个问题。

# 二、解决

自己搜索了半天，终于找到一个靠谱的知乎问题：[用 macOS 自带的 SSH 登陆 Linux 后出现中文乱码，如何解决？](https://www.zhihu.com/question/20117388)

按照提示 `sudo vim /etc/ssh/ssh_config` 之后，注释掉 `SendEnv LANG LC_*` 即可解决。

需要注意的是，该问题每次 MacOS 系统升级之后都需要手动配置一下，似乎每次系统升级都会把 `SendEnv LANG LC_*` 加回去。