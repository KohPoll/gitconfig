# git extra config(git优化配置工具)

`gitconfig`是对`git`的一个优化配置工具，它能解决你的绝大部分“坑爹”问题，提升`git`使用效率。

## 解决的问题

  - 设置全局忽略文件.gitignore，见：<https://github.com/KohPoll/gitconfig/blob/master/res/gitignore>
  - 设置颜色高亮，见：<https://github.com/KohPoll/gitconfig/blob/master/config.d/color>
  - 设置讨厌的跨系统换行符，见：<https://github.com/KohPoll/gitconfig/blob/master/config.d/crlf>
  - 设置写提交日志时的默认编辑器（linux下是vim，windows下是notepad2），见：<https://github.com/KohPoll/gitconfig/blob/master/config.d/editor>
  - 设置讨厌的跨平台编码，见：<https://github.com/KohPoll/gitconfig/blob/master/config.d/encode>
  - 对windows进行更加友好的设置（支持中文输入、diff和merge使用图形工具tortoise，见：<https://github.com/KohPoll/gitconfig/blob/master/config.d/win32>
  - 设置各种舒服的命令缩写，见：<https://github.com/KohPoll/gitconfig/blob/master/config.d/alias>

## 安装方法

首先请安装`git`，安装方法会因平台不同而不同，下面仅提供简要说明，遇到问题，请多用搜索。

  - OSX。推荐使用`brew install git`进行安装，或者下载安装包<http://code.google.com/p/git-osx-installer/downloads/list?can=3>
  - Linux。推荐使用自带的包管理器（如：`yum`，`aptitude`等）安装，或者下载安装包<http://book.git-scm.com/2_installing_git.html>
  - Windows。当然推荐最新版的`msysgit`，下载安装包<http://msysgit.github.io/>有些注意点请大家留意：
    * Configuring the line ending conversions 选项时请保证你选择的是：Checkout Windows-style, commit Unix-style endings 这项
    * 并且一定要将git加入path

### 安装`gitconfig`

  - linux, mac
```
cd ~
git clone https://github.com/KohPoll/gitconfig
cd gitconfig
./gitconfig init
```
  - windows
```
注意：确保[git安装目录/cmd]目录已经加到path下
cd [git安装目录/cmd]
git clone https://github.com/KohPoll/gitconfig
cd gitconfig
bash gitconfig init 
```

### 生成公钥

安装完后，可能需要生成公钥。

方法如下：

  - 首先启动一个Git Bash窗口（非Windows用户直接打开终端），执行`cd ~/.ssh`，如果返回“… No such file or directory”，说明没有生成过SSH Key，直接进入第4步。否则进入第3步备份!
  - 备份：
```
mkdir key_backup
mv id_isa* key_backup
```
  - 生成新的Key：（引号内的内容替换为你自己的*工作邮箱*）
```
ssh-keygen -t rsa -C "your_email@youremail.com"
```
  - 一路回车
  - 提交公钥。找到.ssh文件夹，id_rsa.pub文件即是公钥

## 更新方法

### linux, mac

```
cd ~/gitconfig
./gitconfig update
```

### windows

```
cd [git安装目录/cmd/gitconfig]
bash gitconfig update
```

## 补充说明

在mac下配置后，建议增加以下配置到.bashrc，配置命令行显示git分支、状态、tab建命令补全（针对低版本git）等

```
source ~/gitconfig/res/git-completion.bash

function _git_branch {
    local branch="`git branch 2> /dev/null | grep "^\*" | sed -e "s/^\*\ //"`"
    if [ "${branch}" != "" ];then
        if [ "${branch}" = "(no branch)" ];then
            branch="(`git rev-parse --short HEAD`...)"
        fi
        echo "($branch)"
    fi
}
function _git_status {
    local status="`git status -s 2> /dev/null | tail -n1`"
    if [ "${status}" != "" ];then
        echo "*"
    fi
}
                                                     
export PS1='\[\033[1;32m\]\w\[\033[1;33m\]$(_git_branch)\[\033[1;36m\]$(_git_status) \[\033[1;31m\]-> \[\033[0m\]'
```

## 其他

推荐安装[tig](https://github.com/jonas/tig)，查看log爽飞起。