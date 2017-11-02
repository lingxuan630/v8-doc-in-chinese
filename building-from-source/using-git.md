# Git 仓库

V8的Git仓库地址：https://chromium.googlesource.com/v8/v8.git

V8的master分支在github上有一个官方的镜像：http://github.com/v8/v8-git-mirror

不要通过简单的 `git-clone`这些url来拉去V8的源码，你可以通过一下的步骤来获得：

## 准备工作

1. 安装Git. 在Ubuntu系统可以通过简单的apt-get安装

   ```
   apt-get install git
   ```
   
   在windows，你可以下载安装包: https://git-scm.com/
   
2. depot_tools. 查看具体[安装步骤](http://dev.chromium.org/developers/how-tos/install-depot-tools)

3. 为了能够提交代码，你还需要创建一个.netrc 文件，并且把git密码放进去:

   访问[https://chromium.googlesource.com/new-password](https://chromium.googlesource.com/new-password) ，使用您的提交者帐户登录（例如@ chromium.org帐号，non-chromium.org）。 注意：创建新密码不会自动撤销任何以前创建的密码。 请确保您使用与git config user.email设置的电子邮件相同的电子邮件。看看上面那个大大都灰色框部分的shell命令，然后复制粘贴到你的shell中。
   
## 如何开始

确认你的`depot_tools`已经是最新的，执行下面：

```
gclient
```

然后获取V8，包括所有的分支和依赖

```
mkdir ~/v8
cd ~/v8
fetch v8
cd v8
```

之后你可以切换到你想要的分支了。

或者，您可以指定如何跟踪新分支：

```
git config branch.autosetupmerge always
git config branch.autosetuprebase always
```

或者，您可以这样创建新的本地分支（推荐）

```
git new-branch mywork
```

## 保持更新

通过`git pull`的方式更新你当前的代码，注意，如果你不在一个分支上，pull动作是不生效的，你可以用`git fetch`的方法来代替。

```
git pull
```

有时候V8的依赖包已经更新，你可以通过以下方式更新
```
gclient sync
```

## 发送代码供审核
```
git cl upload
```

## 提交

您可以使用codereview中的CQ复选框来提交（首选）。
