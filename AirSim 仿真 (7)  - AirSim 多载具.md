# AirSim 仿真 (7) - AirSim 多载具

从 release 1.2 开始, AirSim 完全能够支持多载具. 这能允许你更简单的创建多个载具并用 APIs 来控制它们.

## 创建多个载具 Creating Multiple Vehicles

在 [settings.json](settings.md) 可以很简单地对它们设定. `Vehicles` 元素允许你指定你想创建地载具列表, 包括初始位置和方向.位置是基于 SI 单位下的原点位于 Unreal 环境下玩家出生点的 NED 坐标系.方向基于角度制的偏航、俯仰和翻转.

### 创建多辆汽车 Creating Multiple Cars

```json
{
  "SettingsVersion": 1.2,
  "SimMode": "Car",

  "Vehicles": {
    "Car1": {
      "VehicleType": "PhysXCar",
      "X": 4,
      "Y": 0,
      "Z": -2
    },
    "Car2": {
      "VehicleType": "PhysXCar",
      "X": -4,
      "Y": 0,
      "Z": -2,
      "Yaw": 90
    }
  }
}
```

### 创建多个飞行器 Creating Multiple Drones

```json
{
  "SettingsVersion": 1.2,
  "SimMode": "Multirotor",

  "Vehicles": {
    "Drone1": {
      "VehicleType": "SimpleFlight",
      "X": 4,
      "Y": 0,
      "Z": -2,
      "Yaw": -180
    },
    "Drone2": {
      "VehicleType": "SimpleFlight",
      "X": 8,
      "Y": 0,
      "Z": -2
    }
  }
}
```

## 多载具的 APIs 使用 Using APIs for Multiple Vehicles

从 AirSim 1.2 以来的新 APIs 允许你指定 `vehicle_name`. 这个名称和 json settings 的键值对应 (举个例子, 上述的 Car1 或 Drone2 ).

[Example code for cars](https://github.com/Microsoft/AirSim/tree/master/PythonClient//car/multi_agent_car.py)

[Example code for multirotors](https://github.com/Microsoft/AirSim/tree/master/PythonClient//multirotor/multi_agent_drone.py)

**PS:** 这里提供一份 C++ 的实现

```c++
  using namespace msr::airlib;
  msr::airlib::CarRpcLibClient client;

  client.confirmConnection();
  client.enableApiControl(true, "Car1");
  client.enableApiControl(true, "Car2");

  auto car_controls1 = client.getCarControls("Car1");
  auto car_controls2 = client.getCarControls("Car2");

  for (int i = 0; i < 3; ++i) {
    // get state of the car
    auto car_state1 = client.getCarState("Car1");
    std::cout << "Car1: Speed " << car_state1.speed << ", Gear " << car_state1.gear << std::endl;

    auto car_state2 = client.getCarState("Car2");
    std::cout << "Car1: Speed " << car_state2.speed << ", Gear " << car_state2.gear << std::endl;

    // go forward
    car_controls1.throttle = 0.5;
    car_controls2.throttle = 0.5;
    client.setCarControls(car_controls1, "Car1");
    std::cout << "Car1: Go Forward.\n";

    car_controls2.throttle = 0.5;
    car_controls2.steering = -0.5;
    client.setCarControls(car_controls2, "Car2");
    std::cout << "Car2: Go Forward.\n";

    std::this_thread::sleep_for(std::chrono::seconds(3));

    // apply breaks
    car_controls1.brake = 1;
    client.setCarControls(car_controls1, "Car1");
    std::cout << "Car1: Apply break\n";
    car_controls1.brake = 0;  // remove break

    car_controls2.brake = 1;
    client.setCarControls(car_controls2, "Car2");
    std::cout << "Car2: Apply break\n";
    car_controls2.brake = 0;  // remove break

    std::this_thread::sleep_for(std::chrono::seconds(3));  // let car drive a bit

    const std::vector<ImageCaptureBase::ImageResponse>& response1 =
        client.simGetImages({ImageCaptureBase::ImageRequest("0", ImageCaptureBase::ImageType::DepthVis),
                             ImageCaptureBase::ImageRequest("1", ImageCaptureBase::ImageType::Scene, false, false)},
                            "Car1");

    std::cout << "Car1: Retrieved images: " << response1.size() << std::endl;

    const std::vector<ImageCaptureBase::ImageResponse>& response2 =
        client.simGetImages({ImageCaptureBase::ImageRequest("0", ImageCaptureBase::ImageType::Segmentation),
                             ImageCaptureBase::ImageRequest("1", ImageCaptureBase::ImageType::Scene, false, false)},
                            "Car2");

    std::cout << "Car2: Retrieved images: " << response2.size() << std::endl;

    cv::Mat img_mat10 = cv::imdecode(response1.at(0).image_data_uint8, cv::IMREAD_GRAYSCALE);
    cv::imshow("cat1_multi:DepthVis", img_mat10);
    cv::waitKey(5);

    cv::Mat img_mat11(response1.at(1).height, response1.at(1).width, CV_8UC3,
                      (void*)response1.at(1).image_data_uint8.data());
    cv::imshow("cat1_multi:Scene", img_mat11);
    cv::waitKey(5);

    cv::Mat img_mat20 = cv::imdecode(response1.at(0).image_data_uint8, cv::IMREAD_UNCHANGED);
    cv::imshow("cat2_multi:DepthVis", img_mat10);
    cv::waitKey(5);

    cv::Mat img_mat21(response2.at(1).height, response2.at(1).width, CV_8UC3,
                      (void*)response2.at(1).image_data_uint8.data());
    cv::imshow("cat2_multi:Scene", img_mat21);
    cv::waitKey(5);
  }

  client.reset();
  client.enableApiControl(false);
  return 0;
```

### Demo

[![AirSimMultiple Vehicles Demo Video](images/demo_multi_vehicles.png)](https://youtu.be/35dgcuLuF5M)
