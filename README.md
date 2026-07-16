# 第二十一届全国大学生智能汽车竞赛 地瓜机器人-智慧医疗赛项
## 项目简介
本工程为OriginCar智能车完整参赛源码，基于ROS2开发，实现智慧医疗赛道全自主任务：
自主循迹避障、二维码任务读取、医疗目标图像识别、本地大模型图文生成、自主返航。

## 硬件环境
主控：地瓜机器人RDK开发板
车模：OriginCar标准底盘
外设：单目视觉相机（二维码+医疗物品检测）

## 工程目录功能
1. origincar_base：底层底盘电机、运动控制驱动
2. line_follower_pkg：赛道循迹、障碍物避障、自主导航逻辑
3. 3rdparty：图像识别、大模型推理第三方依赖库
4. utils：二维码解析、任务数据处理通用脚本

## 编译

```bash
# 默认工作空间 /userdata/dev_ws/
cd /userdata/dev_ws/
colcon build --symlink-install
```

## 底盘和控制

启动底盘
```bash
ros2 launch origincar_base origincar_bringup.launch.py
```

启动键盘控制
```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```
以下按键进行控制
```
   u    i    o
   j    k    l
   m    ,    .
```
键盘节点会发布 速度消息 到 /cmd_vel 话题，底盘节点订阅速度消息实现键盘控制

## USB 相机驱动与图像可视化
```bash
ros2 launch origincar_bringup usb_websocket_display.launch.py
```
运行成功后，在同一网络的PC端，打开浏览器，输入 http://IP:8000，选择“web展示端”，即可查看图像和算法效果，IP为OriginBot的IP地址。

## 深度相机驱动与图像可视化
启动相机

```bash
ros2 launch deptrum-ros-driver-aurora930 aurora930_launch.py

```
启动rqt_image_view
```
ros2 run rqt_image_view rqt_image_view
```
