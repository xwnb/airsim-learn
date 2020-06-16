# AirSim 仿真 (8) - AirSim 传感器

AirSim 目前支持一下传感器.
每类传感器都与之关联一个整型枚举值来表示传感器类型.

- Camera
- Barometer = 1
- Imu = 2
- Gps = 3
- Magnetometer = 4
- Distance Sensor = 5
- Lidar = 6

**注意** : 相机配置与其他传感器不一样,所以没有关联枚举值. 相机配置和 API 查看 [general settings](settings.md) 和 [image API](image_apis.md) .

## 默认传感器 Default sensors

如果没有在 `settings.json` 指定传感器, 基于 sim 模式下,下列传感器默认可用.

### 载具 Multirotor

- Imu
- Magnetometer
- Gps
- Barometer

### 车 Car

- Gps

### 计算机视觉 ComputerVision

- None

场景之后, [AirSimSettings.hpp](https://github.com/Microsoft/AirSim/blob/master/AirLib/include/common/AirSimSettings.hpp) 中的 `createDefaultSensorSettings` 方法是用来设置上述带默认参数的传感器, 根据在 sim 模式在下 `settings.json` 文件设定的.

## 配置默认传感器列表 Configuring the default sensor list

默认传感器列表可以在 settings json 配置:

```json
"DefaultSensors": {
    "Barometer": {
         "SensorType": 1,
         "Enabled" : true
    },
    "Imu": {
         "SensorType": 2,
         "Enabled" : true
    },
    "Gps": {
         "SensorType": 3,
         "Enabled" : true
    },
    "Magnetometer": {
         "SensorType": 4,
         "Enabled" : true
    },
    "Distance": {
         "SensorType": 5,
         "Enabled" : true
    },
    "Lidar2": {
         "SensorType": 6,
         "Enabled" : true,
         "NumberOfChannels": 4,
         "PointsPerSecond": 10000
    }
},
```

## 配置汽车专用传感器列表 Configuring vehicle-specific sensor list

如果载具提供他自己的传感器列表, 它**必须**提供完整的列表. **不支持** 选择性的增加/删除/更新默认传感器列表
汽车专用传感器列表可以在设置汽车的 json 部分设置.
即,

```json
    "Vehicles": {

        "Drone1": {
            "VehicleType": "SimpleFlight",
            "AutoCreate": true,
            ...
            "Sensors": {
                "MyLidar1": {
                    "SensorType": 6,
                    "Enabled" : true,
                    "NumberOfChannels": 16,
                    "PointsPerSecond": 10000,
                    "X": 0, "Y": 0, "Z": -1,
                    "DrawDebugPoints": true
                },
                "MyLidar2": {
                    "SensorType": 6,
                    "Enabled" : true,
                    "NumberOfChannels": 4,
                    "PointsPerSecond": 10000,
                    "X": 0, "Y": 0, "Z": -1,
                    "DrawDebugPoints": true
                }
            }
        }
   }
```

### 传感器专用设置 Sensor specific settings

每种传感器类型也有它自己的设置.

以雷达专用设定为例,请查看 [lidar](lidar.md) .

## 传感器 APIs Sensor APIs

使用例程可直接跳转到 [`hello_drone.py`](https://github.com/Microsoft/AirSim/blob/master/PythonClient/multirotor/hello_drone.py) 或 [`hello_drone.cpp`](https://github.com/Microsoft/AirSim/blob/master/HelloDrone/main.cpp) , 或者浏览下述全部的 API.

- Barometer

  C++

  ```cpp
  msr::airlib::BarometerBase::Output getBarometerData(const std::string& barometer_name, const std::string& vehicle_name);
  ```

  Python

  ```python
  barometer_data = getBarometerData(barometer_name = "", vehicle_name = "")
  ```

- IMU

  C++

  ```cpp
  msr::airlib::ImuBase::Output getImuData(const std::string& imu_name = "", const std::string& vehicle_name = "");
  ```

  Python

  ```python
  imu_data = getImuData(imu_name = "", vehicle_name = "")
  ```

- GPS

  C++

  ```cpp
  msr::airlib::GpsBase::Output getGpsData(const std::string& gps_name = "", const std::string& vehicle_name = "");
  ```

  Python

  ```python
  gps_data = getGpsData(gps_name = "", vehicle_name = "")
  ```

- Magnetometer

  C++

  ```cpp
  msr::airlib::MagnetometerBase::Output getMagnetometerData(const std::string& magnetometer_name = "", const std::string& vehicle_name = "");
  ```

  Python

  ```python
  magnetometer_data = getMagnetometerData(magnetometer_name = "", vehicle_name = "")
  ```

- Distance sensor

  C++

  ```cpp
  msr::airlib::DistanceBase::Output getDistanceSensorData(const std::string& distance_sensor_name = "", const std::string& vehicle_name = "");
  ```

  Python

  ```python
  distance_sensor_name = getDistanceSensorData(distance_sensor_name = "", vehicle_name = "")
  ```

- Lidar
  See [lidar](lidar.md) for Lidar API.
