# AirSim 仿真 (9) - 如何在 AirSim 使用雷达

针对载具和汽车，AirSim 支持雷达。

可用及其他雷达设定可以通过 AirSimSettings json 配置.
请查看 [general sensors](sensors.md) 获取通用/共享的传感器设置.

## 在汽车上使能雷达 Enabling lidar on a vehicle

- 雷达默认是不可用的。 为了使用雷达， 在 settings json 中设定雷达 SensorType 和 Enabled 属性.

```json
        "Lidar1": {
             "SensorType": 6,
             "Enabled" : true,
```

- 汽车多雷达也可用.

## 雷达配置 Lidar configuration

目前，下列参数可通过 setting json 来配置.

| 参数               | 描述                                                            |
| ------------------ | --------------------------------------------------------------- |
| NumberOfChannels   | 雷达的激光/通道数目                                             |
| Range              | 范围， 米值                                                     |
| PointsPerSecond    | 每秒捕捉的点数                                                  |
| RotationsPerSecond | 每秒旋转角度                                                    |
| HorizontalFOVStart | 雷达初始 Horizontal FOV, 角度制                                 |
| HorizontalFOVEnd   | 雷达终止 Horizontal FOV, 角度制                                 |
| VerticalFOVUpper   | 雷达 Vertical FOV 上限, 角度制                                  |
| VerticalFOVLower   | 雷达 Vertical FOV 下限, 角度制                                  |
| X Y Z              | 雷达相对于汽车的位置 (NED 坐标系, 米制)                         |
| Roll Pitch Yaw     | 雷达相对于汽车的方向 (角度制, 沿 +X 方向的 yaw-pitch-roll)      |
| DataFrame          | 输出的数据坐标系 ("VehicleInertialFrame" 或 "SensorLocalFrame") |

例如,

```json
{
  "SeeDocsAt": "https://github.com/Microsoft/AirSim/blob/master/docs/settings_json.md",
  "SettingsVersion": 1.2,

  "SimMode": "Multirotor",

  "Vehicles": {
    "Drone1": {
      "VehicleType": "simpleflight",
      "AutoCreate": true,
      "Sensors": {
        "LidarSensor1": {
          "SensorType": 6,
          "Enabled": true,
          "NumberOfChannels": 16,
          "RotationsPerSecond": 10,
          "PointsPerSecond": 100000,
          "X": 0,
          "Y": 0,
          "Z": -1,
          "Roll": 0,
          "Pitch": 0,
          "Yaw": 0,
          "VerticalFOVUpper": -15,
          "VerticalFOVLower": -25,
          "HorizontalFOVStart": -20,
          "HorizontalFOVEnd": 20,
          "DrawDebugPoints": true,
          "DataFrame": "SensorLocalFrame"
        },
        "LidarSensor2": {
          "SensorType": 6,
          "Enabled": true,
          "NumberOfChannels": 4,
          "RotationsPerSecond": 10,
          "PointsPerSecond": 10000,
          "X": 0,
          "Y": 0,
          "Z": -1,
          "Roll": 0,
          "Pitch": 0,
          "Yaw": 0,
          "VerticalFOVUpper": -15,
          "VerticalFOVLower": -25,
          "DrawDebugPoints": true,
          "DataFrame": "SensorLocalFrame"
        }
      }
    }
  }
}
```

## 用于调试的服务端可视化 Server side visualization for debugging

默认情况下，雷达点不会被绘制在视图中。 为了能够在视图中绘制激光扫描点， 请通过 settings json 使能 `DrawDebugPoints`.
例如,

```json
        "Lidar1": {
             ...
             "DrawDebugPoints": true
        },
```

## 客户端 API Client API

使用 `getLidarData()` API 来获取雷达数据.

- 这个 API 返回带捕捉时间戳和雷达位置的平面阵列的浮点数数组.
- 点云:
  - 浮点数表示每个在范围之类最后扫描到的 [x,y,z] 坐标.
  - 输出的数据帧可以通过 "DataFrame" 属性来配置。
    "" 或者 "VehicleInertialFrame" -- 默认; 返回汽车惯性坐标系下的点 (NED 坐标系, 米制)
    "SensorLocalFrame" -- 返回雷达局部坐标系下的点 (NED 坐标系, 米制)
- 雷达位姿:
  - 在汽车惯性坐标系下的雷达位姿 (NED 坐标系, 米制)
  - 可以转换到其他坐标系下的点.

### Python 例程 Python Examples

[drone_lidar.py](https://github.com/Microsoft/AirSim/tree/master/PythonClient//multirotor)
[car_lidar.py](https://github.com/Microsoft/AirSim/tree/master/PythonClient//car)

## 即将到来

- 客户端的雷达数据可视化.
