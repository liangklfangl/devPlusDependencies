# npm中script生命周期方法的深入探讨

### 1.Dependencies与devDependencies的合作
如果你想要对你的包在其被使用之前做某种操作，而且这种操作独立于操作系统，那么我们可以使用`preppublish`这个hook,它的主要作用如下：

(1)将CoffeeScript编译成为Javascript

(2)对Javascript代码进行压缩

(3)获取你的包需要加载的远程资源

在prepublish时机这样做的好处是，这些事情都可以立即完成，而且只在一处就可以完成；同时也具有以下好处：

(1)你可以将coffee-script放在devDependencies里面，因此使用该包的人不用下载coffee-script

(2)你的包也不需要依赖于其他的包对文件进行压缩，因此用户也不用安装

(3)你也不需要依赖于包的使用者系统中的curl等系统工具

### 2.批量添加生命周期函数
如果你想对所有的包的某一个生命周期函数都执行一段脚本，那么你可以使用这个方法来完成。你可以将一个可执行文件放在`node_modules/.hooks/{eventname}`里面，那么这个脚本会对所有的该目录下安装的包起作用。但是这段脚本的不同在于，她是在一个独立的子进程中运行的，而且也具有很多[环境变量](https://github.com/liangklfangl/npm-command)。


参考文件：

[npm script](https://docs.npmjs.com/misc/scripts)

[npm command](https://github.com/liangklfangl/npm-command)