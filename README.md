# Quadcopter_Flight_Control
> ROS2 Humble + ArduPilot SITL → Autonomous quadcopter control

## 🎯 Project Overview

This project implements a complete flight control stack for a quadcopter using:
- **ROS2 Humble** - Middleware for node communication
- **ArduPilot** - Flight controller firmware (runs on SITL or real hardware)
- **MAVROS** - ROS2 ↔ MAVLink bridge
- **Gazebo** - Physics simulation

## 🏗️ Architecture

┌─────────────┐     ROS2 Topics      ┌──────────┐     MAVLink      ┌─────────────┐
│  ROS2 Nodes │ ◄──────────────────► │  MAVROS  │ ◄──────────────► │  ArduPilot  │
│  (C++/Py)   │                      │  Bridge  │   (UDP/Serial)   │  (SITL/FC)  │
└─────────────┘                      └──────────┘                  └─────────────┘

## 📦 Package Structure

| Package | Purpose | Status |
|---------|---------|--------|
| `quad_interfaces` | Custom msg/srv/action definitions | 🟡 Planned |
| `quad_mavros_bridge` | MAVROS wrapper + helpers | 🟡 Planned |
| `quad_state_estimator` | Sensor fusion, state estimation | 🟡 Planned |
| `quad_controller` | PID controllers (attitude, position) | 🟡 Planned |
| `quad_mission_planner` | Waypoint, mission logic | 🟡 Planned |
| `quad_safety` | Geofence, failsafe, monitors | 🟡 Planned |
| `quad_bringup` | Launch files, system integration | 🟡 Planned |

## 🗺️ Development Roadmap

| Milestone | Target | Status |
|-----------|--------|--------|
| **M0** Environment Setup | ROS2 + ArduPilot SITL running | 🟢 Done |
| **M1** MAVROS Communication | Arm/disarm via ROS2 service | ⬜ Pending |
| **M2** State Estimation | Position/attitude at 50Hz+ | ⬜ Pending |
| **M3** Basic Control | Takeoff/land/hover in SITL | ⬜ Pending |
| **M4** Position Control | Fly 10m square in SITL | ⬜ Pending |
| **M5** Mission System | Multi-waypoint missions | ⬜ Pending |
| **M6** Safety Systems | Geofence, failsafe, battery | ⬜ Pending |
| **M7** Integration Test | 5-min autonomous flight | ⬜ Pending |
| **M8** Hardware Deploy | Real flight tests | ⬜ Pending |

## 🚀 Quick Start

### Prerequisites
- Ubuntu 22.04
- ROS2 Humble
- ArduPilot (with SITL)
- MAVROS
- Gazebo (optional)

### Build
```bash
cd ~/drone_ws
colcon build
source install/setup.bash
Run Simulation
# Terminal 1: Start SITL
cd ~/ardupilot
Tools/autotest/sim_vehicle.py -v ArduCopter -f gazebo-iris --console --map

# Terminal 2: Start MAVROS
source /opt/ros/humble/setup.bash
ros2 run mavros mavros_node --ros-args -p fcu_url:="udp://:14540@127.0.0.1:14550"

# Terminal 3: Verify connection
ros2 topic echo /mavros/state
📚 Learning Log
This project is built as a learning journey. Each milestone includes:
- Concept explanations before implementation
- Code written from scratch (no copy-paste)
- Unit + integration tests
- Documentation updates
🤝 Contributing
This is a personal learning project, but suggestions welcome via Issues.
📄 License
MIT License - see LICENSE (LICENSE) for details.
