# 针对ARM的交叉编译

## 使用`GN`交叉编译

首先，你可以使用`GN`编译。

然后，添加`android`配置到你的配置文件`.gclient`。
```
target_os = ['android']  # Add this to get Android stuff checked out.
```

`target_os`配置项是一个list, 所以你可以添加更多的适配类型，例如：
```
target_os = ['android', 'unix']  # multiple target oses
```
运行`gclient sync`，然后你会拉取到一堆`checkout`，存放在：`./third_party/android_tools`

在手机和平板上启动开发者模式，然后开启USB调试功能，具体方式可以参考[这里](https://developer.android.com/studio/run/device.html)。而且，你可以在目录中找到[adb](https://developer.android.com/studio/command-line/adb.html)工具，存放在以下目录：
```
./third_party/android_tools/sdk/platform-tools
```

使用`v8gen.py`去生成一个arm release或者debug构建：
```
tools/dev/v8gen.py arm.release
```

然后运行`gn args out.gn/arm.release`，确认已经存在以下keys:
```
target_os = "android"      # These lines need to be changed manually
target_cpu = "arm"         # as v8gen.py assumes a simulator build.
v8_target_cpu = "arm"
is_component_build = false
```
这些keys在debug构建中也是一样的。
