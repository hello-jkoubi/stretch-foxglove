# stretch-foxglove

Use Foxglove with Hello Robot Stretch (ROS 2) for visualization and debugging.

---

# Table of Contents
 - [Requirements](#requirements)
 - [Install](#install)
 - [Test it](#test-it)
 - [Demos](#demos)
 - [Rosbag / MCAP Playback](#rosbag--mcap-playback)

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

> **Note:**
> You can also open it from the `Foxglove` Desktop App 


Once Foxglove opened:

- Click `Open connection`
- Select WebSocket and replace `<robot-ip>` with your robot's IP

	```bash
	ws://<robot-ip>:8765
	```
- Click `Connect`

> **Note:**
> You can retrieve the robot IP using:
> ```bash
> ifconfig wlo1
> ```
> Look for:
> ```bash
> inet <robot-ip>
> ```


## Demos

This section showcases ready-to-use Foxglove layouts for common Stretch workflows.

Each demo is designed to be:

- Quick to launch
- Visually intuitive
- Immediately useful for debugging

Click on any demo to explore setup instructions and details.


### [Demo 1 — Dual Camera View](/docs/demo1.md)

<!-- <div align="center">
  <img src="docs/assets/demo1.gif" alt="base" width="600"/>
</div> -->

<div align="center">
  <a href="/docs/demo1.md">
    <img src="docs/assets/demo1.gif" alt="Demo 1 — Dual Camera View" width="600"/>
  </a>
</div>

### [Demo 2 — Mapping + Teleop](/docs/demo2.md)

<div align="center">
  <img src="docs/assets/demo2.gif" alt="base" width="600"/>
</div>

### [Demo 3 — Stretch ROS 2 System Debugging](/docs/demo3.md)

<div align="center">
  <img src="docs/assets/demo3.gif" alt="base" width="600"/>
</div>

---

## Rosbag / MCAP Playback

Foxglove can replay recorded ROS 2 data for debugging and visualization without needing the robot running.

ROS 2 data can be recorded in two formats:

- rosbag (`.db3`) — the default ROS 2 format
- MCAP (`.mcap`) — a newer, faster, and more portable format that is becoming the standard (and is well supported in Foxglove)

Both formats can be opened and replayed in Foxglove.

### Record Data

- Default ROS 2 rosbag (`.db3`):

	```bash
	ros2 bag record -o <bag_name> </topic1> </topic2>
	```

- MCAP (`.mcap`):

	```bash
	ros2 bag record -s mcap -o <bag_name> </topic1> </topic2>
	```

> **Note:** MCAP requires a one-time installation:
> ```bash 
> sudo apt update
> sudo apt install ros-humble-rosbag2-storage-mcap
> ```

### Open in Foxglove

For this example, we use a pre-recorded ROS 2 bag.

1. Open Foxglove  
2. Click `Open local file(s)`
3. Select the [stretch_debug.db3](bags/stretch_debug/stretch_debug.db3) rosbag


### Visualize the data

Once opened, you can visualize the recorded data by adding panels.

For this example, a layout is already provided.

Load the [multipoint_command_debug.json](layouts/multipoint_command_debug.json) layout to quickly get a full visualization setup.

### Play the recording

Use the playback controls at the bottom of Foxglove to **play the rosbag** and explore the data over time.

<div align="center">
  <img src="docs/assets/rosbag_play.png" alt="base" width="600"/>
</div>

In this example, we use the bag to debug arm joint position.

- On the right-hand side, two plots show the position of two Stretch joints:
	- the **lift joint** (blue)  
	- the **arm joint** (red)  
- At the top right, the full joint states data from the `/joint_states` topic is also displayed.

<div align="center">
  <img src="docs/assets/rosbag-multipoint_command_debug_x2.gif" alt="base" width="600"/>
</div>
