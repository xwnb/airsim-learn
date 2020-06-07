# AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境

对自定义 UE 环境导入 AirSim 插件小车。本文主要参考官方文档 [Creating and Setting Up Unreal Environment](https://microsoft.github.io/AirSim/unreal_custenv/)。



[TOC]

## 地图准备

因为原文使用的一个免费环境在 UE 商城没有找到。不过官方在 `github` 上提供了几个[地图](https://github.com/Microsoft/AirSim/releases)可用，不过下载速度太慢了。所以，本文直接从 UE 的 **学习** tab 下载了一个免费的赛车游戏项目，大概一个G左右。官方提供的几个地图等下载好之后再试试。

<img src="AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607112530427.png" alt="image-20200607112530427" style="zoom:50%;" />



## 创建 UE 工程

1. 点击 `创建工程` 按钮，输入名称和保存的文件夹，`创建` 工程。这里 **不要出现中文路径**， 貌似后面编译老出问题，换成英文之后就过了。

   <img src="AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607113118716.png" alt="image-20200607113118716" style="zoom:50%;" />

2. 打开项目所在文件夹，打开 ue 项目，这里是 `cargame.uproject`. 首次打开估计要编译一会儿，这个看电脑配置，我大概花了 10 分钟 (i7 8700 + GTX 1070Ti + 固态)。

   **PS**：如果使用官方示例中的那个地图，因为没有源码文件，所以触发不了编译。所以官方的那份文档有一步骤是建立一个新的 C++ 的空类。这里不需要，也不能，否则该项目模块编译不了。

   <img src="AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607113756907.png" alt="image-20200607113756907" style="zoom:50%;" />

3. 效果如下图所示，这个是个完整的游戏，如果点击 `运行` 会出来一辆小车，是可以玩的。不过这辆车不是我们要的那辆。

   <img src="AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607115242368.png" alt="image-20200607115242368" style="zoom:50%;" />



## 生成 Visual Studio 项目

1. 在 `UnReal Editor` 中点击 `文件`，`生成Visual Studio项目`。之后，会在项目文件夹下看到一个 vs 项目文件 `cargame.sln`，这里暂时不要打开。先关闭编辑器。

   ![image-20200607115730099](AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607115730099.png)

2. 把 `AirSim` 项目下的 `AirSim` 插件拷贝（路径 `Unreal/Plugins`）到 `cargame` 项目根目录下，如图。

   ![image-20200607121222918](AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607121222918.png)

3. 右键编辑 `cargame.uproject`, 找到 `"Plugins"` 字段，把 `AirSim` 插件添加进去. 保存。

   ```json
   	"Plugins": [
   		{
   			"Name": "PhysXVehicles",
   			"Enabled": true
   		},
   		{
   			"Name": "RawInput",
   			"Enabled": true
   		},
   		{
               "Name": "AirSim",
               "Enabled": true
           }
   	],
   ```

4. 右键 `cargame.uproject`，选择 `Generate Visual Studio project fiels`. 这时候，目录下会出现 vs 的工程文件 `cargame.sln`.

![image-20200607121001231](AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607121001231.png)



5. 打开 vs 工程文件  `cargame.sln`，工程配置为 `DSebugGame Editor`, `Win64`。

![image-20200607121426792](AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607121426792.png)



6. 编译运行工程，成功后，会自动打开 ue 编辑器的，和运行 `Blocks` 示例工程一样。



## 加载 `AirSim` 插件

1. 打开 `世界场景设置` 窗口。如果没有的话，点击 `窗口`，勾选 `世界场景设置` ，即可。效果如下图。

   **PS**: 这里我找了好久，官方文档说默认有的，我这里没有，一直怀疑我安装有啥问题。

   <img src="AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607122150090.png" alt="image-20200607122150090" style="zoom:50%;" />

2. 在 `世界场景设置` 中的 `游戏模式` 的 `游戏模式重载` 下拉框选择 `AirSimGameMode`. 至此所有配置均完成。

   ![image-20200607122408176](AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607122408176.png)



## 运行仿真

在编辑器中点击 `运行` ，然后就出现了我们熟悉的车了，把几个视图窗口调出来。

<img src="AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607122806805.png" alt="image-20200607122806805" style="zoom:50%;" />



## 其他

1. 在编辑器的 `细节` 窗口可以看到选中的 对象的一些信息。比如这里我选中了小车，小车运动时，一些数据能实时变化。

   ![image-20200607123344712](AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607123344712.png)

2. 如果鼠标切换不出来， 按快捷键 `shift + F1`.

3. 鼠标切出时，可能仿真视图界面会出现卡顿的现象。点击 `编辑` -> `编辑器偏好设置……`。搜索一下 `cpu`，把 `编辑器性能` 下的 `处于背景中时占用较少CPU` 的勾勾去掉即可。

   ![image-20200607123712008](AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607123712008.png)

   ![image-20200607123910639](AirSim 仿真 (2) - 创建并设置 Unreal Engine 环境.assets/image-20200607123910639.png)



## 最后

愉快地继续折腾吧。