+++
author = "roiwk"
title = "php使用xdebug进行性能调试"
description = "xdebug性能调试配置与使用"
date = "2023-05-19"
keywords = [
    "xdebug",
    "性能调试",
    "trace",
]
tags = [
    "php",
    "xdebug",
]
categories = [
    "php",
]
draft = true
+++

# php使用xdebug进行性能调试

在开发PHP应用程序时，经常需要进行性能调试以查找和修复代码中的瓶颈。Xdebug是一个强大的工具，能够提供详细的性能分析信息，帮助你找到应用程序中的问题。
# 配置与执行

简单介绍xdebug的安装（如需细节，可查看相关文章，本文主要讲其性能分析功能）

1. pecl安装 [推荐] 

```bash
pecl install xdebug
```

## 配置PHP

安装Xdebug后，我们需要将其启用并配置PHP以与之配合使用。打开php.ini文件，并配置以下行：

```
zend_extension=path/to/xdebug.so

# 配置xdebug, 按需指定ip和端口
xdebug.remote_enable=1
xdebug.remote_autostart=1
xdebug.remote_host=127.0.0.1
xdebug.remote_port=9000

# 主要的性能分析配置
xdebug.profiler_output_dir=/tmp
xdebug.profiler_output_name=cachegrind.out.%t
; xdebug.profiler_enable=1
; xdebug.profiler_enable_trigger=1

```

## 配置IDE

为了能够使用Xdebug进行性能调试，我们还需要将IDE与之集成。这里以[Visual Studio Code](https://code.visualstudio.com/)为例，其他IDE的配置方式可以参考官方文档。

打开VS Code，并安装[PHP Debug](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug)扩展。然后在菜单栏中选择`Debug`->`Add Configuration`，并选择`PHP`作为环境。

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9000
        }
    ]
}
```

接下来，在VS Code中打开要调试的PHP文件，并设置断点。再次打开`Debug`窗口，然后选择`Listen for Xdebug`选项。最后，在浏览器中访问该脚本，并在VS Code中触发相应的操作。

## 分析性能数据

一旦Xdebug捕获了您的代码输出，您就可以开始分析性能数据了。我们使用一个称为[KCacheGrind](https://kcachegrind.github.io/html/Home.html)的桌面工具来显示和分析Xdebug生成的数据。

其他工具：QCacheGrind(与KCacheGrind基本相同) 和 [webgrind](https://github.com/jokkedk/webgrind) (web端的分析工具，有docker端)

之后，打开KCacheGrind并加载callgrind.out(配置文件设置的生成路径可以找到)文件。您将看到一个类似于下面的界面：

![KCacheGrind screenshot]()

在该界面中，您可以看到代码执行期间的函数调用和时间分布图。在左侧窗格中选择一个函数，右侧窗格将显示有关该函数的详细信息。

# 结论

使用Xdebug进行性能调试是一种快速有效的方式，可以帮助您找到应用程序中的瓶颈并优化性能。希望这篇文章能够为您提供一些有用的指导，并使您成为更好的PHP开发人员！

## 遇到的问题+解决

1. webgrind部署后，查看不到文件， 提示 “*storage path...”相关报错。
> 是性能分析文件的文件夹没有权限， 赋予适当权限即可查看。