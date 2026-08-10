# 🕹️ Quadcopter_Flight_Control
> ROS2 Humble + ArduPilot SITL → Autonomous quadcopter control

## 🎯 Project Overview

This project implements a complete flight control stack for a quadcopter using:
- **ROS2 Humble** - Middleware for node communication
- **ArduPilot** - Flight controller firmware (runs on SITL or real hardware)
- **MAVROS** - ROS2 ↔ MAVLink bridge
- **Gazebo** - Physics simulation

## 🏗️ Architecture
```
┌─────────────┐     ROS2 Topics      ┌──────────┐     MAVLink      ┌─────────────┐
│  ROS2 Nodes │ ◄──────────────────► │  MAVROS  │ ◄──────────────► │  ArduPilot  │
│  (C++/Py)   │                      │  Bridge  │   (UDP/Serial)   │  (SITL/FC)  │
└─────────────┘                      └──────────┘                  └─────────────┘
```

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

# 📊 SUMMARY STATS
```
Metric	Count
Total Packages	7
Packages Created	7 🟢
Packages with Code	0 ⬜
Custom Messages	0/6 ⬜
Custom Services	0/3 ⬜
Custom Actions	0/1 ⬜
Launch Files	0/15+ ⬜
Config Files	0/20+ ⬜ 
```

# Order of implementation (dependencies first):
1. quad_interfaces → Define all .msg, .srv, .action
2. quad_mavros_bridge → Wrap MAVROS, publish clean topics
3. quad_state_estimator → Fuse sensors → /quad/state
4. quad_controller → PID → /quad/setpoint_raw
5. quad_mission_planner → Waypoints → trajectory
6. quad_safety → Monitors → failsafe triggers
7. quad_bringup → Integrate all + launch files

## 🚀 Quick Start

### Prerequisites
- Ubuntu 22.04
- ROS2 Humble
- ArduPilot (with SITL)
- MAVROS
- Gazebo (optional)

## *🐍 Pure Python Package Structure*

```
drone_ws/
├── .git/                           🟢 Done
├── .gitignore                      🟢 Done
├── README.md                       🟢 Done
├── LICENSE                         ⬜ Pending
│
├── src/
│   │
│   ├── quad_interfaces/            🟡 IN PROGRESS - MUST be ament_cmake (ROS2 msg gen)
│   │   ├── CMakeLists.txt          🟢 Done
│   │   ├── package.xml             🟢 Done
│   │   ├── msg/                    ⬜ Pending
│   │   ├── srv/                    ⬜ Pending
│   │   └── action/                 ⬜ Pending
│   │
│   ├── quad_mavros_bridge/         ⬜ Pending - ament_python
│   │   ├── setup.py                ⬜ Pending
│   │   ├── setup.cfg               ⬜ Pending
│   │   ├── pyproject.toml          ⬜ Pending
│   │   ├── package.xml             🟢 Done
│   │   ├── resource/               ⬜ Pending
│   │   │   └── quad_mavros_bridge  ⬜ Pending (marker file)
│   │   ├── quad_mavros_bridge/     ⬜ Pending
│   │   │   ├── __init__.py         ⬜ Pending
│   │   │   ├── mavros_wrapper.py   ⬜ Pending
│   │   │   ├── converters.py       ⬜ Pending
│   │   │   ├── state_publisher.py  ⬜ Pending
│   │   │   ├── pose_publisher.py   ⬜ Pending
│   │   │   ├── command_client.py   ⬜ Pending
│   │   │   └── setpoint_publisher.py ⬜ Pending
│   │   └── launch/                 ⬜ Pending
│   │       └── mavros_bridge.launch.py ⬜ Pending
│   │
│   ├── quad_state_estimator/       ⬜ Pending - ament_python
│   │   ├── setup.py                ⬜ Pending
│   │   ├── setup.cfg               ⬜ Pending
│   │   ├── pyproject.toml          ⬜ Pending
│   │   ├── package.xml             🟢 Done
│   │   ├── resource/               ⬜ Pending
│   │   │   └── quad_state_estimator ⬜ Pending
│   │   ├── quad_state_estimator/   ⬜ Pending
│   │   │   ├── __init__.py         ⬜ Pending
│   │   │   ├── state_estimator.py  ⬜ Pending
│   │   │   └── sensor_fusion.py    ⬜ Pending
│   │   ├── config/                 ⬜ Pending
│   │   │   └── ekf_params.yaml     ⬜ Pending
│   │   └── launch/                 ⬜ Pending
│   │       └── state_estimator.launch.py ⬜ Pending
│   │
│   ├── quad_controller/            ⬜ Pending - ament_python
│   │   ├── setup.py                ⬜ Pending
│   │   ├── setup.cfg               ⬜ Pending
│   │   ├── pyproject.toml          ⬜ Pending
│   │   ├── package.xml             🟢 Done
│   │   ├── resource/               ⬜ Pending
│   │   │   └── quad_controller     ⬜ Pending
│   │   ├── quad_controller/        ⬜ Pending
│   │   │   ├── __init__.py         ⬜ Pending
│   │   │   ├── pid_controller.py   ⬜ Pending
│   │   │   ├── attitude_controller.py ⬜ Pending - ~50-100Hz target
│   │   │   ├── position_controller.py ⬜ Pending - ~20-50Hz
│   │   │   └── controller_node.py  ⬜ Pending - Main loop
│   │   ├── config/                 ⬜ Pending
│   │   │   ├── pid_attitude.yaml   ⬜ Pending
│   │   │   └── pid_position.yaml   ⬜ Pending
│   │   └── launch/                 ⬜ Pending
│   │       └── controller.launch.py ⬜ Pending
│   │
│   ├── quad_mission_planner/       ⬜ Pending - ament_python
│   │   ├── setup.py                ⬜ Pending
│   │   ├── setup.cfg               ⬜ Pending
│   │   ├── pyproject.toml          ⬜ Pending
│   │   ├── package.xml             🟢 Done
│   │   ├── resource/               ⬜ Pending
│   │   │   └── quad_mission_planner ⬜ Pending
│   │   ├── quad_mission_planner/   ⬜ Pending
│   │   │   ├── __init__.py         ⬜ Pending
│   │   │   ├── mission_planner.py  ⬜ Pending
│   │   │   ├── waypoint_navigator.py ⬜ Pending
│   │   │   └── trajectory_generator.py ⬜ Pending
│   │   ├── config/                 ⬜ Pending
│   │   │   └── mission_params.yaml ⬜ Pending
│   │   ├── missions/               ⬜ Pending
│   │   │   ├── square.yaml         ⬜ Pending
│   │   │   ├── figure8.yaml        ⬜ Pending
│   │   │   └── survey.yaml         ⬜ Pending
│   │   └── launch/                 ⬜ Pending
│   │       └── mission_planner.launch.py ⬜ Pending
│   │
│   ├── quad_safety/                ⬜ Pending - ament_python
│   │   ├── setup.py                ⬜ Pending
│   │   ├── setup.cfg               ⬜ Pending
│   │   ├── pyproject.toml          ⬜ Pending
│   │   ├── package.xml             🟢 Done
│   │   ├── resource/               ⬜ Pending
│   │   │   └── quad_safety         ⬜ Pending
│   │   ├── quad_safety/            ⬜ Pending
│   │   │   ├── __init__.py         ⬜ Pending
│   │   │   ├── geofence.py         ⬜ Pending
│   │   │   ├── battery_monitor.py  ⬜ Pending
│   │   │   ├── failsafe_manager.py ⬜ Pending
│   │   │   └── health_monitor.py   ⬜ Pending
│   │   ├── config/                 ⬜ Pending
│   │   │   ├── geofence.yaml       ⬜ Pending
│   │   │   └── failsafe.yaml       ⬜ Pending
│   │   └── launch/                 ⬜ Pending
│   │       └── safety.launch.py    ⬜ Pending
│   │
│   └── quad_bringup/               ⬜ Pending - ament_python
│       ├── setup.py                ⬜ Pending
│       ├── setup.cfg               ⬜ Pending
│       ├── pyproject.toml          ⬜ Pending
│       ├── package.xml             🟢 Done
│       ├── resource/               ⬜ Pending
│       │   └── quad_bringup        ⬜ Pending
│       ├── launch/                 ⬜ Pending
│       │   ├── bringup.launch.py   ⬜ Pending
│       │   ├── simulation.launch.py ⬜ Pending
│       │   ├── hardware.launch.py  ⬜ Pending
│       │   └── components/         ⬜ Pending
│       ├── config/                 ⬜ Pending
│       │   ├── system_params.yaml  ⬜ Pending
│       │   └── sim_params.yaml     ⬜ Pending
│       └── scripts/                ⬜ Pending
│           ├── sitl_setup.sh       ⬜ Pending
│           └── hardware_setup.sh   ⬜ Pending
│
├── config/                         ⬜ Pending
├── docs/                           ⬜ Pending
├── scripts/                        ⬜ Pending
├── test/                           ⬜ Pending
│   ├── unit/                       ⬜ Pending - pytest
│   ├── integration/                ⬜ Pending
│   └── simulation/                 ⬜ Pending
└── docker/                         ⬜ Pending
```
# 🔗 WORKING COMMAND CHAIN 
```
Terminal | 	Command	                                                                                                                | Purpose
1	     | cd ~/ardupilot && Tools/autotest/sim_vehicle.py -v ArduCopter -f gazebo-iris --console --map	                            | Start ArduCopter SITL + Gazebo
2	     | source /opt/ros/humble/setup.bash && ros2 run mavros mavros_node --ros-args -p fcu_url:="udp://:14540@127.0.0.1:14550"	|  MAVROS bridge (UDP:14550)
3	     | source /opt/ros/humble/setup.bash && ros2 topic echo /mavros/state	                                                    | Verify connected: true
```

# 📡 KEY MAVROS TOPICS
```
Category     | 	Topic	Type	                                         | Direction
State	     | /mavros/state	mavros_msgs/State	                     | FC → ROS2
Position     | /mavros/global_position/global	sensor_msgs/NavSatFix    | FC → ROS2
Position	 | /mavros/local_position/pose	geometry_msgs/PoseStamped    | FC → ROS2
Attitude	 | /mavros/imu/data	sensor_msgs/Imu	                         | FC → ROS2
Attitude	 | /mavros/attitude	geometry_msgs/QuaternionStamped	         | FC → ROS2
Command	     | /mavros/setpoint_raw/local	mavros_msgs/PositionTarget	 | ROS2 → FC
Control	     | /mavros/cmd/arming	mavros_msgs/CommandBool	             | ROS2 → FC
Control	     | /mavros/set_mode	mavros_msgs/SetMode	                     | ROS2 → FC 
```
# 🎮 FLIGHT MODES FOR OFFBOARD CONTROL
```
Mode	              | Controller	             | Use Case
STABILIZE	          | Pilot (RC)	             | Manual flight, rate control
GUIDED	              | ArduPilot internal	     | Waypoint navigation (FC computes trajectory)
OFFBOARD	          | Your ROS2 node	         | External setpoints at >2Hz (PID in ROS2)
AUTO	              | ArduPilot mission	     | Pre-loaded waypoint mission
RTL	                  | ArduPilot	             | Return to Launch (safety)
LAND	              | ArduPilot	             | Auto-land
```

# 🔑 Key Python-Specific Files
```
## setup.py (replaces CMakeLists.txt)
from setuptools import find_packages, setup

package_name = 'quad_mavros_bridge'

setup(
    name=package_name,
    version='0.0.1',
    packages=find_packages(exclude=['test']),
    data_files=[
        ('share/ament_index/resource_index/packages',
            ['resource/' + package_name]),
        ('share/' + package_name, ['package.xml']),
        ('share/' + package_name + '/launch', ['launch/mavros_bridge.launch.py']),
    ],
    install_requires=['setuptools'],
    zip_safe=True,
    maintainer='aditya',
    maintainer_email='aditya@example.com',
    description='MAVROS bridge wrapper for quadcopter',
    license='MIT',
    tests_require=['pytest'],
    entry_points={
        'console_scripts': [
            'state_publisher = quad_mavros_bridge.state_publisher:main',
            'pose_publisher = quad_mavros_bridge.pose_publisher:main',
            'command_client = quad_mavros_bridge.command_client:main',
            'setpoint_publisher = quad_mavros_bridge.setpoint_publisher:main',
        ],
    },
)

## package.xml (Python deps)

<depend>rclpy</depend>
<depend>mavros_msgs</depend>
<depend>geometry_msgs</depend>
<depend>quad_interfaces</depend>
<test_depend>ament_copyright</test_depend>
<test_depend>ament_flake8</test_depend>
<test_depend>ament_pep257</test_depend>
<test_depend>pytest</test_depend>

## pyproject.toml (modern config)

[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[tool.pytest.ini_options]
pythonpath = ["src"]

[tool.black]
line-length = 100
target-version = ['py310']
``` 
# ⚠️ One Exception: quad_interfaces  
```
Must remain ament_cmake because ROS2 message generation (.msg, .srv, .action → Python/C++ classes) only works with CMake.
##This package stays as-is (already created with ament_cmake)
src/quad_interfaces/
├── CMakeLists.txt      # Required for rosidl_generate_interfaces()
├── package.xml
├── msg/
├── srv/
└── action/
All other packages: ament_python with setup.py
```
# 🐍 Python Performance Tips for Control Loops
```
Technique 	                | Why	                                          | Example
Use numpy	                | Vectorized math, 10-50x faster than loops	      | np.array([1,2,3]) * 2
Pre-allocate arrays	        | Avoid GC pauses in control loop	              | self.error = np.zeros(3)
Single-threaded executor    |	Predictable timing	                          | rclpy.executors.SingleThreadedExecutor()
time_ns() for timing	    | Nanosecond precision	                          | self.get_clock().now().nanoseconds
Avoid allocations in loop	| No list.append(), no new objects	              | Reuse self.msg object
Profile with cProfile	    | Find bottlenecks	                              | python -m cProfile -o prof.out node.py
```

# 🗺️ Development Roadmap



### **M0: Environment Setup & Verification** ✅
**Foundation** — Establish the complete simulation-to-ROS2 pipeline.

**Deliverables**
- ROS2 Humble, MAVROS, ArduPilot SITL, Gazebo installed and verified
- SITL ↔ MAVROS ↔ ROS2 communication chain working (`connected: true`)
- GitHub repository initialized with professional structure

## Build

```bash
cd ~/drone_ws
colcon build
source install/setup.bash
Run Simulation

# Terminal 1: Start SITL & Gazebo
gnome-terminal -- bash -c 'gz sim -v4 -r iris_runway.sdf; exec bash' &
cd ~/ardupilot
Tools/autotest/sim_vehicle.py -v ArduCopter -f gazebo-iris --model JSON --console --map

# Terminal 2: Start MAVROS
ros2 run mavros mavros_node --ros-args -p fcu_url:="udp://127.0.0.1:14550@" -p target_system_id:=1 -p target_component_id:=1

# Terminal 3: Verify connection
ros2 topic echo /mavros/state
```

**Concepts Mastered**
Quadcopter physics · PID theory · MAVLink protocol · MAVROS bridge · SITL vs hardware · Coordinate frames (ENU/NED/FRD) · Flight modes

---

### **M1: MAVROS Communication & Basic Commands**
**Abstraction Layer** — Clean ROS2 API over MAVROS; full vehicle command authority.

**Deliverables**
- Custom interfaces: `DroneState`, `Waypoint`, `ArmDisarm`, `SetMode`, `TakeoffLand`, `ExecuteMission`
- MAVROS wrapper node: state/pose publishers, command services, setpoint publisher
- Verified arm/disarm, mode switching, OFFBOARD entry/exit via ROS2 services

**Concepts Mastered**
ROS2 interfaces (msg/srv/action) · MAVROS service mapping · OFFBOARD requirements · Frame conversion (ENU↔NED) · QoS profiles

---

### **M2: State Estimation & Sensor Fusion**
**Perception** — Fused, high-rate state estimate with covariance.

**Deliverables**
- Complementary filter or EKF fusing IMU + GPS + barometer
- `/quad/state` (DroneState) at 50Hz+ with meaningful covariance
- Sensor quality monitoring and dropout handling

**Concepts Mastered**
Sensor models · Complementary filter / EKF · Noise characterization · Covariance tuning · Time synchronization

---

### **M3: Basic Flight Control (Takeoff/Hover/Land)**
**Control** — Cascaded PID loops achieving stable hover.

**Deliverables**
- Position (outer) → Attitude (inner) → Motor mixer control stack
- Stable hover at target position for 30+ seconds (XY < 0.3m, Z < 0.2m)
- Takeoff → hover → land sequence via service calls
- Emergency stop from any state

**Concepts Mastered**
Cascaded control architecture · PID tuning · Motor mixing (X-config) · Anti-windup · Feedforward (gravity compensation)

---

### **M4: Position Control & Waypoint Navigation**
**Guidance** — Fly arbitrary 3D trajectories with precision.

**Deliverables**
- Waypoint follower with acceptance radius and velocity limits
- Trajectory generator: smooth paths (polynomial splines)
- Predefined missions: square, figure-8, circle
- Dynamic waypoint updates mid-flight

**Concepts Mastered**
Path following (pure pursuit, L1, Stanley) · Trajectory generation · Waypoint acceptance logic · Local↔global coordinate transforms

---

### **M5: Mission System & Autonomy**
**Autonomy** — Complete mission executive with QGroundControl integration.

**Deliverables**
- Mission state machine: IDLE → ARM → TAKEOFF → WAYPOINTS → RTL/LAND
- Action server for `ExecuteMission` with feedback (current WP, ETA)
- Complex missions: survey grid, orbit, region-of-interest
- Pause/resume/abort via ROS2 actions

**Concepts Mastered**
Behavior trees / state machines · MAVLink mission protocol · Action server pattern · Error handling (unreachable WP, timeout)

---

### **M6: Safety Systems & Failsafes**
**Reliability** — Autonomous protection against failures.

**Deliverables**
- Geofence: cylinder/polygon boundary → breach triggers RTL
- Battery monitor: 3-level failsafe (warn → RTL → land now)
- Link loss detection: heartbeat timeout → RTL
- Health monitor: GPS quality, EKF status, sensor health

**Concepts Mastered**
Failsafe hierarchy · Battery modeling · Geofence math · MAVLink heartbeat monitoring

---

### **M7: Integration Testing & Simulation Campaign**
**Validation** — Verified, regression-tested, performant system.

**Deliverables**
- Unit tests (pytest) for each package
- Integration tests: full stack bringup, mission flow
- SITL scenario tests: 5-min autonomous flight with wind/disturbances
- CI/CD pipeline: build → test → SITL integration on every push
- Performance profiling: CPU, memory, loop timing

**Concepts Mastered**
ROS2 testing (ament_pytest, launch_testing) · Headless SITL automation · GitHub Actions · Profiling (cProfile, snakeviz)

---

### **M8: Hardware Deployment & Real Flight**
**Deployment** — From simulation to sky.

**Deliverables**
- Companion computer setup (RPi 4 / Jetson Orin): ROS2 + MAVROS + FC serial link
- Hardware-specific launch files and parameter configs
- Pre-flight checklist, tethered bench test, flight procedures
- First outdoor autonomous flights: hover → square mission

**Concepts Mastered**
Companion computer architecture · UART/USB MAVLink link · Parameter management · Safety pilot procedures · Regulatory compliance

---






## Author

**Aditya Yadav**
Engineering student exploring embedded systems, robotics, and ROS2.

## License

This project is open source and available under the [MIT License](LICENSE).

