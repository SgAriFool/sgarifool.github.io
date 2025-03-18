---
layout: post
title: 安装Windows11后再安装ArchLinux时EFI分区如何挂载
date: 2025-03-18
tags:
  - linux
  - arch
comments: true
author: sgarifool
toc: false
---

> 本篇 blog 为安装 Windows11 和 ArchLinux 双系统时对于, EFI 分区挂如何挂载问题的记录, 系统的安装顺序是先安装 Windows11 再安装 ArchLinux, 并且两个系统安装在同一个硬盘上

<!-- more -->

## 写在前面话

由于我先安装的 Windows11 并且一开始没有仔细考虑, 后面需要安装 Arch 这件事情, 所以对于我来说, 安装好的 Windows11 的 EFIsystem 分区大小只有默认的 100mb. 如果你此时只有一个硬盘, 并且已经确定需要先安装 Win 再安装 Arch, 可以参考官方链接 [Arch+Windows双系统](https://wiki.archlinuxcn.org/zh-hans/Arch_%2B_Windows_%E5%8F%8C%E7%B3%BB%E7%BB%9F) 的第 2.3.5 小结, 在安装 Win 的时候可以将系统的 EFI 分区手动分大一点, 比如 1G, 那么按照网上的任何教程, 不管是将 efi 分区挂载在 `/mnt/boot/` 下, 还是在 `/mnt/efi` 下都没有问题, 因为 EFI 分区足够大, 但是如果的 Win 已经下好, 并且你不想重装系统, 那么可以参考一下下面的内容. 前面部分讲的是为什么, 如果希望直接看结果, 可以跳到最后

## 关于 Win 下的 EFI 分区的目录结构

想要查看 Win 下 EFI 分区的目录结构, 可以使用 Win 自带的 `diskpart` 工具[^1]

使用管理员权限打开 Win 的终端: 右键启动图标, 可以看到圈出来的终端管理员

![](../assets/img-2025-03-18-how_to_mount_efi_partitions.png)

输入命令

```bash
diskpart
```

进入 `distpart` 工具, 然后输入

```bash
list disk
```

查询硬盘信息, 找到 Win 的系统盘所在磁盘(可以根据所列出来磁盘的大小判断), 输入命令

```bash
select disk 0 # 这里我的输出只有一个磁盘, 如果不一样请改成自己的
```



## 参考文献

[^1]: https://blog.csdn.net/mtllyb/article/details/78635757

