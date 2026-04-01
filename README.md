# stretch-foxglove

Use Foxglove with Hello Robot Stretch (ROS 2) for visualization and debugging.

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

#### 1. Launch stretch driver (Robot)

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
