# AirSim 仿真 (3) - 配置 Visual Studio 工程 - C++

接下来的文章主要开始记录 AirSim 提供的 APIs 的学习。但是在自己新建一个工程的时候发现，配置有很多问题，这里先解决一下。

在第一篇文章【AirSim 仿真 (1) - Windows 10 下安装仿真平台 AirSim - v1.3.1】，跑了一下示例工程 `Hello Car` . 因为工程配置的关系，发现吧这个工程拷贝出来后，在打开编译不了。但是自己码工程的时候，目录不一定非得限制到 AirSim 的工程目录下吧，总归自己有个文件夹的。

其实看一下 `Hello Car` 的工程属性配置可以看到其实编译不了的原因，无非是包含目录、依赖库的关系。因此，这里主要解决一下这些配置问题。

---

[TOC]

---

## 新建工程

1. 创建一个控制台应用，指定一个自己的归档路径。过程不叙述了。这里，我新建了一个`car-controller` 文件夹（和 `AirSim` 项目不在一起）。工程就叫做 `CarController`.

   ![image-20200607165137306](<AirSim%20%E4%BB%BF%E7%9C%9F%20(3)%20-%20%E9%85%8D%E7%BD%AE%20Visual%20Studio%20%E5%B7%A5%E7%A8%8B.assets/image-20200607165137306.png>)

2. 把示例程序 `HelloCar` 的源码拷贝过来，不用想，这里肯定都是满屏的错误。
3. 整个过程其实和配置 `OpenCV`的过程差不多，开始配置项目工程属性，进入 `项目` -> `属性`。

## 添加附加包含目录

1. `配置属性` -> `C/C++` -> `常规` -> `附加包含目录`

2. 添加如下三个包含目录，在 `AirSim` 工程内。我这里是 `D:\dev\airsim_ws\airsim`

   > `$(airsim项目目录)\AirLib\deps\rpclib\include`
   >
   > `$(airsim项目目录)\AirLib\deps\eigen3`
   >
   > `$(airsim项目目录)\AirLib\include`

   ![image-20200607170319035](<AirSim%20%E4%BB%BF%E7%9C%9F%20(3)%20-%20%E9%85%8D%E7%BD%AE%20Visual%20Studio%20%E5%B7%A5%E7%A8%8B.assets/image-20200607170319035.png>)

## 添加附加库目录

1. `配置属性` -> `链接器` -> `常规` -> `附加库目录`

2. 添加如下三个包含库目录，在 `AirSim` 工程内。

   > `$(airsim项目目录)\AirLib\lib\$(Platform)\$(Configuration)`
   >
   > `$(airsim项目目录)\AirLib\deps\rpclib\lib\$(Platform)\$(Configuration)`
   >
   > `$(airsim项目目录)\AirLib\deps\MavLinkCom\lib\$(Platform)\$(Configuration)`

3. **PS**: 因为 `Windows` 下的库区分 `Debug` 和 `Release`模式，还有 `x86` 和 `x64` 连个平台。

   > `$(Platform)` : 这个就是区分 `Debug` 和 `Release`的
   >
   > `$(Configuration)` : 这个区分 `x86`还是 `x64`的

![image-20200607171024035](<AirSim%20%E4%BB%BF%E7%9C%9F%20(3)%20-%20%E9%85%8D%E7%BD%AE%20Visual%20Studio%20%E5%B7%A5%E7%A8%8B.assets/image-20200607171024035.png>)

## 配置附加依赖项

完成上一步，这时候代码应该不会冒红了，但是编译还是过不了的。会包 `LNK2019` 无法解析的外部符号的错误，因为依赖库找不到。

1. `配置属性` -> `链接器` -> `输入` -> `附加依赖项`

2. 添加库，上一步的三个 `lib` 文件夹下的库都需要添加进去。**PS**: 还有一种方法针对很多库的，比如 `OpenCV` 是不是在这里要添加很多库，有些时候还会漏掉导致工程编译失败。这里也又一个小技巧，就是用通配符，把指定目录下的所有 lib 都添加进来。

   > `$(airsim项目目录)\AirLib\deps\rpclib\lib\$(Platform)\$(Configuration)\*.lib` > `$(airsim项目目录)\AirLib\deps\MavLinkCom\lib\$(Platform)\$(Configuration)\*.lib` > `$(airsim项目目录)\AirLib\lib\$(Platform)\$(Configuration)\*.lib`

![image-20200607175949310](<AirSim%20%E4%BB%BF%E7%9C%9F%20(3)%20-%20%E9%85%8D%E7%BD%AE%20Visual%20Studio%20%E5%B7%A5%E7%A8%8B.assets/image-20200607175949310.png>)

## 编译运行

工程配置： `Debug`, `x64`。例程再次跑起来了。

![image-20200607182009709](<AirSim%20%E4%BB%BF%E7%9C%9F%20(3)%20-%20%E9%85%8D%E7%BD%AE%20Visual%20Studio%20%E5%B7%A5%E7%A8%8B.assets/image-20200607182009709.png>)

## 其他

其实到这里，如果有编译好的库和插件，其实都不需要下载 UE （除非要自定义场景）或者源码编译。

这里把我编译好的库文件和插件上传了，可自行下载:

> AirLib-v1.3.1-vs2019.zip
>
> Plugins-AirSim-v1.3.1-ue2.25.1.zip

地图的话，在官方的 `github` 上可以自己[下载](https://github.com/microsoft/AirSim/releases): <https://github.com/microsoft/AirSim/releases>，里面是打包好的应用程序，双击就可以运行，可以下载一个小地图试试。

**PS**：如果是汽车的话就不要下载 `ZhangJiaJie`那幅图了，给无人机用的，车开不了。

![image-20200607183454753](<AirSim%20%E4%BB%BF%E7%9C%9F%20(3)%20-%20%E9%85%8D%E7%BD%AE%20Visual%20Studio%20%E5%B7%A5%E7%A8%8B.assets/image-20200607183454753.png>)

## 最后

接下去就要开始正真的开发使用了……
