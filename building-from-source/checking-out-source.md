# 通过命令行访问

## Git

具体请查看[使用git](https://github.com/v8/v8/wiki/Using-Git)

## 源码分支管理 

在V8代码仓库中有几个不同的分支，如果你不确定你要获取的是哪一个分支，那么就直接获取最新的stable版本。可以阅读一下我们的[发布进度](https://github.com/v8/v8/wiki/Release-process)，以便了解更多关于分支版本的使用。

你可能希望跟进在chrome上已经稳定（或者beta）的V8版本，请浏览：http://omahaproxy.appspot.com

## V8公共接口(public api)的兼容性

V8的公共接口（一般是在`include/`下面的文件夹）可能会随时间而变化。在不破坏现在的功能前提下，可能新增数据类型或者方法。如果我们决定弃用一些类或者方法，我们首先会使用[V8_DEPRECATED](https://code.google.com/p/chromium/codesearch#search/&q=V8_DEPRECATED&sq=package:chromium&type=cs)来标记它。如果调用这些准备弃用的方法时，编译器会报warining。我们会保留准备弃用的方法一个版本的时间，在下一个版本发布时会移除它。例如，如果`v8::CpuProfiler::FindCpuProfile`在3.17版本没有标记为弃用，但是在3.18版本中标记为`V8_DEPRECATED`，那么在3.19版本很可能就移除了。

我们会为每个版本维护一份[“重要API变更的文档”](https://docs.google.com/document/d/1g8JFi8T_oAE_7uAri7Njtig7fKaPDfotU6huOa1alds/edit)



