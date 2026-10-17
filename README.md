# teleop_joy_ctrl

## 作用

ROS1 手柄遥操作节点，控制底盘速度、机械臂状态、相机参数、补光灯和视频录制。

## 运行

配置文件：`config/default.yaml`。主启动文件会按需启动速度复用、手柄控制、补光灯和视频管理节点。

```bash
roslaunch teleop_joy_ctrl teleop_joy_ctrl.launch
```

常用参数：`robot_ip`、`joy_topic`、`cmd_vel_topic`、`start_arm_bringup`、`start_light_controller`、`start_video_manager` 和 `start_takeover_mux`。

## 接口

订阅：

- `/joy_teleop/joy` (`sensor_msgs/Joy`)：手柄输入。
- 相机曝光/增益状态、视频状态和输出目录话题。

发布：

- `/teleop_joy_ctrl/cmd_vel` (`geometry_msgs/Twist`)：底盘速度。
- `/teleop_joy_ctrl/state`、`/teleop_joy_ctrl/debug` (`std_msgs/String`)：控制状态和调试信息。
- `/camera/exposure_cmd`、`/camera/gain_cmd`：相机参数控制。
- `/light/power_cmd`、`/light/brightness_cmd`：补光灯控制。
- `/light/serial_state`、`/light/serial_debug`：补光灯状态。

视频服务：

- `/teleop_joy_ctrl/video/start`
- `/teleop_joy_ctrl/video/pause`
- `/teleop_joy_ctrl/video/resume`
- `/teleop_joy_ctrl/video/stop`

以上视频服务使用 `std_srvs/Trigger`，分别用于开始、暂停、恢复和停止录制。机械臂控制服务由 `dobot_v4_bringup` 提供。
