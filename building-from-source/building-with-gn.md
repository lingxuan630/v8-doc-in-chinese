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

### 基于封装的简易方式
使用一些方便的封装后的脚本来生成文件，例如：
```
tools/dev/v8gen.py x64.release
```
调用`v8gen.py --help`获取更多信息，你可以通过调用`v8gen`来调用脚本，也可以在其他`checkout`中使用它。

以下列举了一些可用配置：
`tools/dev/v8gen.py list`
`tools/dev/v8gen.py list -m client.v8`

### 原始方式

首先创建必要的构建文件：
```
gn args out.gn/foo
```
这时候将打开编辑器以指定[gn参数](https://chromium.googlesource.com/chromium/src/+/master/tools/gn/docs/reference.md)。你可以把`foo`更改任意的文件夹。请注意，我们使用一个单独的`out.gn`文件夹，以避免与旧的gyp文件夹相冲突。如果你不使用gyp或者保持子文件夹分离，你可以使用`out`。

其实你也可以再命令行上传递参数：

```
gn gen out.gn/foo --args='is_debug=false target_cpu="x64" v8_target_cpu="arm64"  use_goma=true'
```

上面的命令会生成构建文件，以使用goma进行编译在release模式下通过arm64模拟器编译V8。可以通过以下方式查看所有`gn`的参数：

```
gn args out.gn/foo --list
```

## 编译
编译一个全量的v8可以通过以下方式（假设gn生成到x64.release文件夹）：
```
ninja -C out.gn/x64.release
```

如果要编译一个特定的版本，例如d8,可以添加到命令行

```
ninja -C out.gn/x64.release d8
```

## 测试

您可以将输出目录传递给测试驱动程序。 其他相关flags将从构建中带出来：

```
tools/run-tests.py --outdir out.gn/foo
```

你也可以测试你最近编译的版本(在 `out.gn`):

```
tools/run-tests.py --gn
```
