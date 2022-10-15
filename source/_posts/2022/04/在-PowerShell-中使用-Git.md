---
title: 在 PowerShell 中使用 Git
categories:
  - 未分类
tags:
  - 无标签
date: 2022-04-22 18:18:21
---

## 前言

在 macOS 下 git 命令行工具默认有着很好的 tab 补全功能，而在 Windows 下通过 exe 安装的 git 程序，看起来就有些简陋。

其自带的 Unix Shell 环境模拟窗口 Git Bash，有着丑陋的外观，即便可以通过配置字体、颜色等手段稍加改善，但其一会儿类 Unix 工具链环境的反馈，一会儿 Windows cmd 工具链混搭的集成环境，着实容易让人精神分裂。

为了更好的自始至终统一使用体验，我们通常会将 git 程序添加到 全局 path 中（引导安装程序即可选配），然后在 cmd 或 PowerShell（通常是功能更强大的 PowerShell）中调用 git。

然而在 PowerShell 中调用 git 时，我们丧失了 tab 补全功能。

这里，我们介绍使用 [Posh-Git](https://github.com/dahlbyk/posh-git) 这个扩展包，从而在 PowerShell 中应用 git 的 tab 补全。

## 安装 Post-Git

### 配置脚本执行权限

在可以运行 PowerShell 脚本之前，你需要将本地的 ExecutionPolicy 设置为 RemoteSigned

在 PowerShell 中执行下面的命令，更精细化的配置参见 [微软文档 Set-ExecutionPolicy](https://learn.microsoft.com/zh-cn/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-7.2)

```
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
```

### 使用包管理器安装 posh-git

在 PowerShell 中执行下面的命令，通过包管理器来安装 posh-git

```
Install-Module posh-git -Scope CurrentUser -Force
Install-Module posh-git -Scope CurrentUser -AllowPrerelease -Force # 带有 PowerShell Core 支持的更新的 beta 版
```

如果你想为所有的用户安装 posh-git，请使用 `-Scope AllUsers` 并在管理员权限启动的 PowerShell 控制台中执行。

### 更新 PowerShell 提示符

要在你的提示符中包含 Git 信息，那么需要导入 Posh-Git 模块。 要让 PowerShell 在每次启动时都导入 Posh-Git，请执行 `Add-PoshGitToProfile` 命令， 它会在你的 $profile 脚本中添加导入语句。此脚本会在每次打开新的 PowerShell 终端时执行。

```
Import-Module posh-git
Add-PoshGitToProfile -AllHosts
```

更多详细内容，参见：[Git 文档：A1.9 附录 A: 在其它环境中使用 Git - Git 在 PowerShell 中使用 Git](https://git-scm.com/book/zh/v2/附录-A%3A-在其它环境中使用-Git-Git-在-PowerShell-中使用-Git)

## 顺便说下中文乱码问题

PowerShell 下 `git log` 中文、`git status` 文件名等，可能存在中文乱码的问题。

可以向下面一样配置 git：

```
git config --global core.quotepath false
git config --global gui.encoding utf-8
git config --global i18n.commit.encoding utf-8
git config --global i18n.logoutputencoding utf-8
```

