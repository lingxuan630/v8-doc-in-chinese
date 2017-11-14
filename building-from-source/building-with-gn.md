# 使用GN构建

遇到构建问题？可以在[code.google.com/p/v8/issues](https://code.google.com/p/v8/issues) 上报bug，或者通过邮件联系我们: v8-users@googlegroups.com

## 构建V8

V8是通过[GN](https://chromium.googlesource.com/chromium/src/+/master/tools/gn/docs)构建的。GN是能适应各种情景的构建系统，因为它能为其他的构建系统生成文件。你如何构建取决于你正在使用的“后端”构建系统和编译器。下面的说明文档是假设你已经[下载了V8源代码](https://github.com/lingxuan630/v8-doc-in-chinese/blob/master/building-from-source/using-git.md)，但还没有安装构建需要的依赖。

如果你计划在V8上开发，例如是发布补丁或者处理checklist上的任务，你需要安装依赖。

更多关于GN的信息，你可以阅读[chromium文档](https://www.chromium.org/developers/gn-build-configuration)或者[GN的官网](https://chromium.googlesource.com/chromium/src/+/master/tools/gn/docs)

## 先决条件：构建依赖

可以通过以下命令获取到构建依赖:
```
gclient sync
```
而GN是通过[depot_tools](https://www.chromium.org/developers/how-tos/install-depot-tools)分发的。

## 构建

可以通过两种方式构建V8。一种是使用较低级别的命令行的原始方式，另外一种是使用封装的脚本的简易方式。

构建说明(基于封装的简易方式)
使用一些方便的封装后的脚本来生成文件，例如：
```
tools/dev/v8gen.py x64.release
```
调用`v8gen.py --help`获取更多信息
