# AirSim 仿真 (6) - 设置

接下去主要介绍一下 `AirSim` 的配置参数, 主要翻译了 [官方](https://microsoft.github.io/AirSim/settings) 文档.

---

[TOC]

---

## 设置保存在哪儿? Where are Settings Stored

Windows: `Documents\AirSim`
Linux: `~/Documents/AirSim`

文件格式通常为 [json format](https://en.wikipedia.org/wiki/JSON). 在首次启动 AirSim 是将创建 `settings.json` 文件, 不含任何设置. 为了避免产生问题, 通常使用 ASCII 格式来保存 json 文件.

## 如何选择汽车还是飞行器? How to Chose Between Car and Multirotor

默认设置是飞行器. 要使用汽车, 则设置 `"SimMode": "Car"` :

```json
{
  "SettingsVersion": 1.2,
  "SimMode": "Car"
}
```

选择汽车, 则设置 `"SimMode": "Multirotor"`. 如果想让用户选择载具类型, 则设置 `"SimMode": ""`.

## 可用设置及默认值 Available Settings and Their Defaults

下述是完整的可用设置参数及其默认值的列表. 如果在 json 文件中没有设置参数, 则会使用默认值. 有些默认参数简单地指定为 `""`, 表示实际参数值需要你根据实际使用的载具来选择. 举个例子, `ViewMode` 默认参数为 `""` , 针对飞行器转换成 `"FlyWithMe"`, 针对汽车则是 `"SpringArmChase"` .

**警告:** 不要把拷贝下面的文本到你自己的 settings.json. 我们强烈建议只加入你不想设置为默认值的参数. 唯一需要设置的元素是 `"SettingsVersion"`.

```json
{
  "SimMode": "",
  "ClockType": "",
  "ClockSpeed": 1,
  "LocalHostIp": "127.0.0.1",
  "RecordUIVisible": true,
  "LogMessagesVisible": true,
  "ViewMode": "",
  "RpcEnabled": true,
  "EngineSound": true,
  "PhysicsEngineName": "",
  "SpeedUnitFactor": 1.0,
  "SpeedUnitLabel": "m/s",
  "Recording": {
    "RecordOnMove": false,
    "RecordInterval": 0.05,
    "Cameras": [
        { "CameraName": "0", "ImageType": 0, "PixelsAsFloat": false, "Compress": true }
    ]
  },
  "CameraDefaults": {
    "CaptureSettings": [
      {
        "ImageType": 0,
        "Width": 256,
        "Height": 144,
        "FOV_Degrees": 90,
        "AutoExposureSpeed": 100,
        "AutoExposureBias": 0,
        "AutoExposureMaxBrightness": 0.64,
        "AutoExposureMinBrightness": 0.03,
        "MotionBlurAmount": 0,
        "TargetGamma": 1.0,
        "ProjectionMode": "",
        "OrthoWidth": 5.12
      }
    ],
    "NoiseSettings": [
      {
        "Enabled": false,
        "ImageType": 0,

        "RandContrib": 0.2,
        "RandSpeed": 100000.0,
        "RandSize": 500.0,
        "RandDensity": 2,

        "HorzWaveContrib":0.03,
        "HorzWaveStrength": 0.08,
        "HorzWaveVertSize": 1.0,
        "HorzWaveScreenSize": 1.0,

        "HorzNoiseLinesContrib": 1.0,
        "HorzNoiseLinesDensityY": 0.01,
        "HorzNoiseLinesDensityXY": 0.5,

        "HorzDistortionContrib": 1.0,
        "HorzDistortionStrength": 0.002
      }
    ],
    "Gimbal": {
      "Stabilization": 0,
      "Pitch": NaN, "Roll": NaN, "Yaw": NaN
    }
    "X": NaN, "Y": NaN, "Z": NaN,
    "Pitch": NaN, "Roll": NaN, "Yaw": NaN
  },
  "OriginGeopoint": {
    "Latitude": 47.641468,
    "Longitude": -122.140165,
    "Altitude": 122
  },
  "TimeOfDay": {
    "Enabled": false,
    "StartDateTime": "",
    "CelestialClockSpeed": 1,
    "StartDateTimeDst": false,
    "UpdateIntervalSecs": 60
  },
  "SubWindows": [
    {"WindowID": 0, "CameraName": "0", "ImageType": 3, "Visible": false},
    {"WindowID": 1, "CameraName": "0", "ImageType": 5, "Visible": false},
    {"WindowID": 2, "CameraName": "0", "ImageType": 0, "Visible": false}
  ],
  "SegmentationSettings": {
    "InitMethod": "",
    "MeshNamingMethod": "",
    "OverrideExisting": false
  },
  "PawnPaths": {
    "BareboneCar": {"PawnBP": "Class'/AirSim/VehicleAdv/Vehicle/VehicleAdvPawn.VehicleAdvPawn_C'"},
    "DefaultCar": {"PawnBP": "Class'/AirSim/VehicleAdv/SUV/SuvCarPawn.SuvCarPawn_C'"},
    "DefaultQuadrotor": {"PawnBP": "Class'/AirSim/Blueprints/BP_FlyingPawn.BP_FlyingPawn_C'"},
    "DefaultComputerVision": {"PawnBP": "Class'/AirSim/Blueprints/BP_ComputerVisionPawn.BP_ComputerVisionPawn_C'"}
  },
  "Vehicles": {
    "SimpleFlight": {
      "VehicleType": "SimpleFlight",
      "DefaultVehicleState": "Armed",
      "AutoCreate": true,
      "PawnPath": "",
      "EnableCollisionPassthrogh": false,
      "EnableCollisions": true,
      "AllowAPIAlways": true,
      "RC": {
        "RemoteControlID": 0,
        "AllowAPIWhenDisconnected": false
      },
      "Cameras": {
        //same elements as CameraDefaults above, key as name
      },
      "X": NaN, "Y": NaN, "Z": NaN,
      "Pitch": NaN, "Roll": NaN, "Yaw": NaN
    },
    "PhysXCar": {
      "VehicleType": "PhysXCar",
      "DefaultVehicleState": "",
      "AutoCreate": true,
      "PawnPath": "",
      "EnableCollisionPassthrogh": false,
      "EnableCollisions": true,
      "RC": {
        "RemoteControlID": -1
      },
      "Cameras": {
        "MyCamera1": {
          //same elements as elements inside CameraDefaults above
        },
        "MyCamera2": {
          //same elements as elements inside CameraDefaults above
        },
      },
      "X": NaN, "Y": NaN, "Z": NaN,
      "Pitch": NaN, "Roll": NaN, "Yaw": NaN
    }
  }
}
```

## 仿真模式 SimMode

SimMode 决定了将使用哪种仿真模式. 目前支持一下参数值:

- `""`: 提示用户选择载具类型, 飞行器或者汽车
- `"Multirotor"`: 使用飞行器仿真
- `"Car"`: 使用汽车仿真
- `"ComputerVision"`: 只用摄像头, 没有载具和物理 (**PS**: 应该泛指物理碰撞、接触之类的交互)

## 视角模式 ViewMode

ViewMode 决定哪儿相机被设置为默认以及相机如何跟随载具 (**PS:** 就是在用户的观察视角, 而不是载具摄像头的视角). 对于无人机, 默认 ViewMode 是`"FlyWithMe"` , 汽车的 ViewMode 是 `"SpringArmChase"`.

- `FlyWithMe`: 从 6 个自由度跟随
- `GroundObserver`: 在 XY 平面内自由跟随.
- `Fpv`: 载具前部摄像机视角 (**PS:** 第一人称, 汽车的话就是驾驶室人眼的位置)
- `Manual`: 不会自动移动摄像机. 通过方向键和 ASWD 键来移动摄摄像机.
- `SpringArmChase`: 通过以固定在载具上以弹簧杆 (不可见)相连的摄像机视角跟随 (所以看起来有点延迟) (**PS**: 相当于在载具上装了根延长杆 (类似手持的拍照杆), 延长杆有点弹性, 导致载具起步时, 视角有种被拽着一起动的感觉) .
- `NoDisplay`: 这将冻结主屏幕的渲染, 但是对子窗口、录频及 APIs 的渲染依然激活. (**PS**: UE 里面子窗口好像也是黑的, 但是 APIs 可以调用出来图像). 在那些你只关心获取到的图像而不关心如何在主屏幕渲染的 “无用” 模式下, 这个模式能节省资源. 这也可以提高录像图像的 FPS.

## 时间 TimeOfDay

该设置控制环境中太阳的位置. 默认 `Enabled` 是 false, 意味这太阳的位置无论何时太阳都在场景的左侧并且一直不变. 如果 `Enabled` 是 true, 那么太阳的位置将会通过在 `OriginGeopoint` 节点中设定的经度, 纬度, 高度结合在 `StartDateTime` 设定的时间来计算. `StartDateTime` 是一串 [%Y-%m-%d %H:%M:%S](https://en.cppreference.com/w/cpp/io/manip/get_time) 格式的字符串, 举个例子, `2018-02-12 15:20:00`. 如果字符串为空, 那么就用当前的日期和时间. 如果 `StartDateTimeDst` 是 true, 那么我们将调整白天时长. 太阳的位置根据 `UpdateIntervalSecs`设定的时间间隔来持续更新. 在某些情况下, 可能希望天体时钟可以比仿真始终更快或者更慢. 这可以通过`CelestialClockSpeed`设置, 举个例子, 值 100 意味这仿真时钟 1 秒, 太阳的位置将提前 100 秒, 所以天空中的太阳看起来移动的更加快了.

**PS:** 怎么设置太阳都没有动, 改变时间倒是太阳的起始点位置变了.

参考 [Time of Day API](apis.md#time-of-day-api).

## 地理原点 OriginGeopoint

这个将设置玩家出生点在 Unreal 环境中的经度, 维度, 高度. 载具的原点通过这个值来转换. 记住所有通过 APIs 的坐标系都是基于国际标准单位制的 NED 坐标系统. 这意味着每个载具都开始于 NED 坐标系下的 (0, 0, 0) 点. 每日的时间设置也是根据`OriginGeopoint` 设定的地理坐标系计算.

## 子窗口 SubWindows

这个设定指定按下 0 键显示的 3 个子窗口. WindowsID 可以是 0 到 2, CameraName 可以是载具上的任何一个 [可用的相机](image_apis.md#available_cameras). ImageType 的值根据 [ImageType enum](image_apis.md#available-imagetype) 决定显示哪类图片. 举个例子, 对于下面的载具, 分别显示了驾驶员视角, 前视角, 后视角的场景, 深度, 分割图像. .

```json
  "SubWindows": [
    {"WindowID": 0, "ImageType": 0, "CameraName": "3", "Visible": true},
    {"WindowID": 1, "ImageType": 3, "CameraName": "0", "Visible": true},
    {"WindowID": 2, "ImageType": 6, "CameraName": "4", "Visible": true}
  ]
```

## 记录 Recording

记录功能允许你已设定的时间间隔采集类似位置, 方向, 速度的图像. 你可以通过按下红色的 Recored 按钮或者 R 键来开始记录. 数据将被保存在 `Documents\AirSim` 文件夹中, 每个记录会话都放在一个时间戳命名的子文件中, 以 tab 分割的文本 (**PS:** 举个例子, Record 的数据被保存在已时间戳命名的文件夹中 `2020-06-14-13-43-41` 文件夹中, 图片放在 `image` 子文件夹中, 数据放在 `airsim_rec.txt` 文本文件中, 文本以 Tab 分割).

- `RecordInterval`: 设定采样图片的最小间隔, 秒.
- `RecordOnMove`: 设定在载具位置和姿态没有变化的时候不要采集.
- `Cameras`: 控制采集哪个相机的图像. 默认的采集 camera 0 的压缩的 png 格式的场景图像. 这个设定是一个 json 数组的形式, 所以你可以指定采集多个相机不同[image types](settings.md#image-capture-settings)的图像, 当 PixelsAsFloat 是 true, 图像将被以 [pfm](pfm.md) 格式保存而不是 png.

## 时钟速度 ClockSpeed

这个设置将允许你设置仿真的时钟. 举个例子, 5.0 表示当挂钟过了 1 秒, 仿真时间过了 5.0 秒 (即仿真运行更快了). 值 0.1 表示仿真比挂钟慢了 10X. 值 1 表示仿真时间和真实时间一样. 当仿真时钟运行更快的情况下, 仿真质量可能降低, 意识到这点很重要. 所以你可能看到一些物体穿模, 因为碰撞没有被探测到. 然后, 降低仿真时钟 (即值 < 1.0) 通常能提高仿真质量.

## 分割设置 Segmentation Settings

`InitMethod` 决定如何在启动的时候初始化 object IDs 来生成 [segmentation](image_apis.md#segmentation). 值 `""` 或者 `"CommonObjectsRandomIDs"` (默认) 意味着在启动时给每个 object 分配随机的 IDs. 生成的分割图中, 每个 object 也被分配为随机的颜色. 值 `"None"` 意味这不初始化 object IDs. 这将造成分割视图只有单一固定的颜色. 如果你计划通过 [APIs](image_apis.md#segmentation) 来设置 object IDs 会有用. 这也能节约大场景的启动延时, 像 CityEnviron.

如果 `OverrideExisting` 是 `false`, 那么初始化时不会改变已分配的非零的 object IDs , 否则会.

如果 `MeshNamingMethod` 为 `""` 或者 `"OwnerName"` , 那么我们用网格拥有者的名字来生成随机哈希值作为 object IDs. 如果是`"StaticMeshName"` , 那么我们用静态的网格名称来生成随机哈希值作为 object IDs. 记住这种方法通常不能区分相同静态网格的单个实例, 但是名称通常更加直观.

## 相机设置 Camera Settings

`CameraDefaults` 作为所有相机设置的根节点元素. 默认值可以被 `Vehicles` 中的 `Cameras` 元素中的单个相机设置覆盖.

### Note on ImageType element

JSON 数组的`ImageType` 元素决定哪种图像类型将被运用. 可用的值在图像类型那一节说明过. 此外, 我们也支持特殊的值 `ImageType: -1` , 来对外部相机设置 (即你在屏幕上看到的场景视角).

举个例子, `CaptureSettings` 元素是 json 数组, 所以你可以很容易地添加多个图像类型的设置.

### 捕捉设置 CaptureSettings

`CaptureSettings` 决定如何渲染不同的图像类型, 比如 scene, depth, disparity, surface normals 和 segmentation. 宽度, 高度, FOV 的设置应该无需多言. `AutoExposureSpeed`决定眼睛的适应速度多快 (**PS**: 自动曝光速度?) . 通常我们设定一个较大值, 比如 100 来避免图像采集中的假影. 类似地, 我们默认设置 `MotionBlurAmount` 为 0 来避免地面图像地假影. `ProjectionMode` 决定采集的相机用的投影模式, 该值可以是 `"perspective`" (默认) 或者 `"orthographic"`. 如果投影模式是 `"orthographic"` , 那么`OrthoWidth` 决定以米制宽度来采集投影区域.

更多其他设置, 请参考 [this article](https://docs.unrealengine.com/latest/INT/Engine/Rendering/PostProcessEffects/AutomaticExposure/).

(**PS:** 这里不太懂, 没有图像相关的知识)

### 噪声设置 NoiseSettings

`NoiseSettings` 允许对指定的图像类型增加噪声, 通过模拟相机传感器的噪声, 干涉和其他假影. 默认美哟添加噪声 即 `Enabled: false`. 如果你设置 `Enabled: true` , 那么不同类型的噪声, 干涉, 假影生效, 每个都可以被进一步设置. 噪声的效果通过在 Unreal 引擎中后期材质处理是添加阴影来实现, 称为 [CameraSensorNoise](https://github.com/Microsoft/AirSim/blob/master/Unreal/Plugins/AirSim/Content/HUDAssets/CameraSensorNoise.uasset).

相机的噪声和干涉仿真的例子:

[![AirSim Drone Demo Video](images/camera_noise_demo.png)](https://youtu.be/1BeCEZmQyp0)

#### 随机噪声 Random noise

这将通过下述参数来增加随机噪声斑点.

- `RandContrib`: 这决定了噪声像素与图像像素的混合比率, 0 表示没有噪声, 1 表示只有噪声.
- `RandSpeed`: 这决定了噪音波动的速度, 1 表示没有波动, 高值如 1E6 表示完全波动.
- `RandSize`: 这决定了噪声的粗糙程度, 1 表示每个像素都有自己的噪声, 较大的值表示多个像素有相同的噪声值.
- `RandDensity`: 这决定了有多少像素会有噪声, 1 表示所有像素都有噪声, 较高的值意味着较少的像素 (指数).

#### Horizontal bump distortion

这增加了水平凸起/闪烁/重影效果.

- `HorzWaveContrib`: 这决定了噪声像素与图像像素的混合比率, 0 表示没有噪声, 1 表示只有噪声
- `HorzWaveStrength`: 这决定了该影响的整体强度.
- `HorzWaveVertSize`: 这决定了有多少垂直像素会受到影响
- `HorzWaveScreenSize`:这决定了有大的屏幕受影响

#### Horizontal noise lines

这在水平线上增加了噪声区域.

- `HorzNoiseLinesContrib`: 这决定了噪声像素与图像像素的混合比率, 0 表示没有噪声, 1 表示只有噪声
- `HorzNoiseLinesDensityY`: 这决定了水平线中有多少像素会受到影响.
- `HorzNoiseLinesDensityXY`: 这决定了屏幕上有多少行会受到影响.

#### Horizontal line distortion

这增加了水平线上的波动.

- `HorzDistortionContrib`: 这决定了噪声像素与图像像素的混合比率, 0 表示没有噪声, 1 表示只有噪声.
- `HorzDistortionStrength`: 这决定了失真的强度

### 云台 Gimbal

`Gimbal` 元素允许冻结相机的俯仰, 翻转, 偏航. 这个设置会被忽略, 除非 `ImageType` 是 -1. `Stabilization` 默认设置为 0 , 意味着没有云台, 即相机在所有轴上都随着物体发生变化. 值 1 意味着完全稳定. 介于 0 到 1 之间的值作为对在 `Pitch`, `Roll` 和`Yaw` 元素被指定的固定角度 (角度, 世界坐标系) 和载具的方向的权重. 当任一角度被省略或者设置为 `NaN`, 那么这个角度是不稳定的 (即随着物体而运动).

**PS**: 应该是云台

## 载具设置 Vehicles Settings

每种仿真模式将遍历在该设置中的载具列表, 然后创建那些 `"AutoCreate": true` 的载具. 每个被设定的载具有个成为该载具名称的键值. 如果 `"Vehicles"` 元素缺省, 那么这个列表将被填入名为 `"PhysXCar"` 的默认汽车和名为 `"SimpleFlight"` 默认飞行器.

### 通用载具设置 Common Vehicle Setting

- `VehicleType`: 可以是 `PhysXCar`, `SimpleFlight`, `PX4Multirotor` 或者 `ComputerVision`. 这个没有默认值, 所以必须被指定.
- `PawnPath`: 这个允许覆盖载具使用的 pawn blueprint. 举个例子, 你可以创建一个新的 pawn blueprint , 继承于 ACarPawn, 作为你自己项目中而不在 AirSim 代码中的仓储机器人, 然后在这里指定路径. 参见 [PawnPaths](#PawnPaths).
- `DefaultVehicleState`: 飞行器可用的值为 `Armed` 或 `Disarmed`.
- `AutoCreate`: 如果为 true, 那么这个载具将被加载 (如果选中的 sim 模式支持.
- `RC`: 这个子元素允许通过`RemoteControlID`指定载具使用哪个远程控制器. 值 -1 意味着使用键盘 (飞行器暂时不支持). 值 >= 0 指定被连接上的远程控制器其中的一个. 举个例子, 在 Window 中, 可用的 RCs 列表可以在 Game Controllers 面板中看到.
- `X, Y, Z, Yaw, Roll, Pitch`: 这个元素允许你指定载具的初始位置和方向. 位置是在 SI 单位制 NED 坐标系中, 坐标系原点被设置在 Unreal 环境中的玩家出生点. 方向以角度指定.
- `IsFpvVehicle`: 这个设置允许指定哪个载具的摄像头被跟随. 当 `ViewMode` 被设置为 `Fpv` 时, 这个视角将被显示. 默认情况下, AirSim 选择设置中的第一个载具作为 FPV 载具.
- `Cameras`: 这个元素设定载具的相机设置. 这个元素中的关键是 [available camera](image_apis.md#available_cameras) 的名称, 这个值和上述 `CameraDefaults` 的一致. 举个例子, 为了改变前面中间相机 FOV 为 120 度, 你可以用这个 `Vehicles` 设置:

```json
"Vehicles": {
    "FishEyeDrone": {
      "VehicleType": "SimpleFlight",
      "Cameras": {
        "front-center": {
          "CaptureSettings": [
            {
              "ImageType": 0,
              "FOV_Degrees": 120
            }
          ]
        }
      }
    }
}
```

### Using PX4

By default we use [simple_flight](simple_flight.md) so you don't have to do separate HITL or SITL setups. We also support ["PX4"](px4_setup.md) for advanced users. To use PX4 with AirSim, you can use the following for `Vehicles` setting:

```json
"Vehicles": {
    "PX4": {
      "VehicleType": "PX4Multirotor",
    }
}
```

#### Additional PX4 Settings

The defaults for PX4 is to enable hardware-in-loop setup. There are various other settings available for PX4 as follows with their default values:

```json
"Vehicles": {
    "PX4": {
      "VehicleType": "PX4Multirotor",

      "ControlIp": "127.0.0.1",
      "ControlPort": 14580,
      "LogViewerHostIp": "127.0.0.1",
      "LogViewerPort": 14388,
      "OffboardCompID": 1,
      "OffboardSysID": 134,
      "QgcHostIp": "127.0.0.1",
      "QgcPort": 14550,
      "SerialBaudRate": 115200,
      "SerialPort": "*",
      "SimCompID": 42,
      "SimSysID": 142,
      "TcpPort": 4560,
      "UdpIp": "127.0.0.1",
      "UdpPort": 14560,
      "UseSerial": true,
      "UseTcp": false,
      "VehicleCompID": 1,
      "VehicleSysID": 135,
      "Model": "Generic",
      "LocalHostIp": "127.0.0.1"
    }
}
```

These settings define the MavLink SystemId and ComponentId for the Simulator (SimSysID, SimCompID), and for the vehicle (VehicleSysID, VehicleCompID)
and the node that allows remote control of the drone from another app this is called the offboard node (OffboardSysID, OffboardCompID).

If you want the simulator to also talk to your ground control app (like QGroundControl) you can also set the UDP address for that in case you want to run
that on a different machine (QgcHostIp, QgcPort). The default is local host so QGroundControl should "just work" if it is running on the same machine.

You can connect the simulator to the LogViewer app, provided in this repo, by setting the UDP address for that (LogViewerHostIp, LogViewerPort).

And for each flying drone added to the simulator there is a named block of additional settings. In the above you see the default name "PX4". You can change this name from the Unreal Editor when you add a new BP_FlyingPawn asset. You will see these properties grouped under the category "MavLink". The MavLink node for this pawn can be remote over UDP or it can be connected to a local serial port. If serial then set UseSerial to true, otherwise set UseSerial to false. For serial connections you also need to set the appropriate SerialBaudRate. The default of 115200 works with Pixhawk version 2 over USB.

When communicating with the PX4 drone over serial port both the HIL*\* messages and vehicle control messages share the same serial port.
When communicating over UDP or TCP PX4 requires two separate channels. If UseTcp is false, then UdpIp, UdpPort are used to send HIL*\* messages,
otherwise the TcpPort is used. TCP support in PX4 was added in 1.9.2 with the `lockstep` feature because the guarantee of message delivery that
TCP provides is required for the proper functioning of lockstep. AirSim becomes a TCP server in that case, and waits for a connection
from the PX4 app. The second channel for controlling the vehicle is defined by (ControlIp, ControlPort) and is always a UDP channel.

## 其他设置 Other Settings

### 引擎声音 EngineSound

通过设置 [setting](settings.md) `"EngineSound": false` 来关闭引擎声音. 目前这个设置只在汽车上运用.

### PawnPaths

This allows you to specify your own vehicle pawn blueprints, for example, you can replace the default car in AirSim with your own car. Your vehicle BP can reside in Content folder of your own Unreal project (i.e. outside of AirSim plugin folder). For example, if you have a car BP located in file `Content\MyCar\MySedanBP.uasset` in your project then you can set `"DefaultCar": {"PawnBP":"Class'/Game/MyCar/MySedanBP.MySedanBP_C'"}`. The `XYZ.XYZ_C` is a special notation required to specify class for BP `XYZ`. Please note that your BP must be derived from CarPawn class. By default this is not the case but you can re-parent the BP using the "Class Settings" button in toolbar in UE editor after you open the BP and then choosing "Car Pawn" for Parent Class settings in Class Options. It's also a good idea to disable "Auto Possess Player" and "Auto Possess AI" as well as set AI Controller Class to None in BP details. Please make sure your asset is included for cooking in packaging options if you are creating binary.

### 物理引擎名称 PhysicsEngineName

对于汽车, 我们目前只支持 `PhysX` (忽略这是设置值), 对于飞行器, 我们只支持 `"FastPhysicsEngine"` .

### 本地主机 IP 设置 LocalHostIp Setting

当你需要连接到远程主机, 你需要通过以太网适配器来互联, 举个例子, 可能通过以太网或者 Wi-Fi, 或者其他一些虚拟适配器或者 VPN. 你的 PC 可能有多个网络, 这些网络可能不孕寻互相通讯, 这种情况下, UDP 消息就不能传播到其他主机上. 所以 `LocalHostIp`允许你配置如何连接这些主机. 默认值 127.0.0.1 不能够到达外部主机, 这个默认值只能用来单个主机内部通讯.

### 速度单位因子 SpeedUnitFactor

速度转换成`m/s`因子, 默认为 1. 与 `SpeedUnitLabel` 结合使用. 这通常只被用来显示, 比如汽车行驶速度显示. 举个例子, 速度转换到 `miles/hr` 的因子是 2.23694.

### 速度单位标签 SpeedUnitLabel

速度单位, 默认为 `m/s`. 结合 `SpeedUnitFactor` 一起使用.
