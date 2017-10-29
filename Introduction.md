
欢迎来到V8开发者文档。V8是Google开源的高性能JavaScript引擎，它是用C++语言编写的，并被应用在Google的Chrome浏览器中。

文档主要是面向那些希望在应用程序中使用V8引擎的C++开发者，当然对V8引擎的设计和性能感兴趣的开发者也可以参考本文档。本文将向您介绍V8，其余文档将向您介绍如何在代码中使用V8，并介绍其一些设计细节，同时也会提供一些用于测量V8性能的JavaScript基准测试。

## 关于V8

V8是根据[ECMA-262](https://www.ecma-international.org/publications/standards/Ecma-262.htm)第五版规范来实现ECMAScript的，并在Windows（XP或更高版本），Mac OS X（10.5或更高版本）以及使用IA-32，x64或ARM处理器的Linux系统上运行。

V8编译并执行JavaScript源代码，处理对象的内存分配，回收不再需要的对象。V8的stop-the-world(从应用中停下来并进入到GC执行过程中去),以及使用分代(Generational Collection)的精确内存垃圾回收机制，是性能优化的关键要素之一。您可以在V8设计原理中了解到垃圾回收以及其他方面的性能优化。

JavaScript主要被用作浏览器的客户端脚本语言，例如用来操作DOM(Document Object Model).DOM是在浏览器提供的，JavaScript引擎并没有内置DOM。V8引擎也是如此 - Google Chrome提供了DOM。不过，V8提供了ECMA标准中指定的所有数据类型，操作符，对象和函数。

通过V8引擎，素有C++编写的程序都可以将自己的对象和函数公开给JavaScript代码调用。至于公开哪些对象或者函数完全由你来决定。事实上有很多应用程序已经是这样做了，例如苹果Mac OS X和Yahoo!中的Adobe Flash和仪表板小部件小工具。
