# stretch-foxglove

Use Foxglove with Hello Robot Stretch (ROS 2) for visualization and debugging.

---

# Table of Contents
 - [Requirements](#requirements)
 - [Install](#install)
 - [Test it](#test-it)
 - [Demos](#demos)



---

## Requirements

### Host (Laptop)
- Foxglove Studio (desktop or browser)
- Same network as robot

### Robot (Stretch)
- ROS 2 (tested with Humble)
- Running Stretch ROS 2 stack

---

## Install

### Host — Foxglove Studio

Foxglove Studio is available on:
- Linux
- Windows
- macOS

In this guide, we use a Linux host.

Download the **x64 version** from:
https://foxglove.dev/download

Install:

```bash
sudo dpkg -i foxglove-studio-*.deb
sudo apt-get install -f
```

Test launch:

```bash
foxglove-studio
```

On first launch, you will need to sign in / log in.

### Stretch Robot — Foxglove Bridge

```bash
sudo apt update
sudo apt install ros-humble-foxglove-bridge
```

---

## Test it

#### 1. Launch Stretch Driver (Robot)

```bash
ros2 launch stretch_core stretch_driver.launch.py
```
	
#### 2. Launch Bridge (Robot)

```bash
ros2 launch foxglove_bridge foxglove_bridge_launch.xml
```

#### 3. Connect (Host)

Launch Foxglove:

```bash
foxglove-studio
```

> Note:
> You can also open it from the `Foxglove` Desktop App 


Once Foxglove opened:

- Click `Open connection`
- Select WebSocket and replace `<robot-ip>` with your robot's IP

	```bash
	ws://<robot-ip>:8765
	```
- Click `Connect`

> Note:
> You can retrieve the robot IP using:
> ```bash
> ifconfig wlo1
> ```
> Look for:
> ```bash
> inet <robot-ip>
> ```


## Demos

This section includes ready-to-use Foxglove layouts for common Stretch workflows.

Each demo is designed to be quick to launch and immediately useful for visualization and debugging.
 
You will learn how to load a layout to visualize it in Foxglove.

---

### Load a layout

1. Open Foxglove Studio on your host computer
2. Go to `Layouts` (left sidebar)
3. Click `+ Add` 
4. Select `Import Personal Layout`
5. Choose the layout file (`.json`) located at `stretch-foxglove/layouts`
6. The layout will be added to the Layouts list, select it and click `Open`

---

### Demo 1 — Dual Camera View

<div align="center">
  <img src="docs/demo-multi-camera.png" alt="base" width="600"/>
</div>

1. Launch the Foxglove Bridge (Robot):

```bash
ros2 launch foxglove_bridge foxglove_bridge_launch.xml
```

2. Run Stretch Driver:

```bash
ros2 launch stretch_core stretch_driver.launch.py
```

3. Run the Dual Camera pipeline:

```bash
ros2 launch stretch_core multi_camera.launch.py 
```

4. Load the `stretch_dual_camera.json` layout in Foxglove.

That's it, you can now visualize your data in Foxglove.


#### What you’ll see

- Head (D435i) + gripper (D405) camera feeds
- Both streams updating in real time
- Side-by-side comparison for quick debugging
- Live robot diagnostics (ROS 2 `/diagnostics`)
- Homing status indicator
- Runstop (safety) status

---

### Demo 2 — Mapping + Teleop

<div align="center">
  <img src="docs/demo-mapping.png" alt="base" width="600"/>
</div>

1. Launch the Foxglove Bridge (Robot):

```bash
ros2 launch foxglove_bridge foxglove_bridge_launch.xml
```

2. Run the Mapping pipeline:

```bash
ros2 launch stretch_nav2 offline_mapping.launch.py use_rviz:=false
```

3. Load the `stretch_mapping.json` layout in Foxglove.

#### What you’ll see

- Live map building as the robot moves
- Robot odometry + laser scan
- Teleop panel to drive the robot
- Live robot diagnostics (ROS 2 `/diagnostics`)
- Homing status indicator
- Runstop (safety) status
