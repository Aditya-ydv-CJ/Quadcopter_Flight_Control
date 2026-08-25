
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



# **M0: Environment Setup & Verification** ✅
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

##  @MAVLink Protocol — Quick Reference

**What it is:** A lightweight, binary messaging protocol for talking to drones/vehicles — used between the autopilot, ground control stations, and companion computers (like MAVROS). Transport-agnostic: runs over serial, UDP, or TCP.

**Addressing**
- Every node has a `system_id` + `component_id` — e.g. `1.1` = vehicle system 1 / autopilot component; `1.191` = same vehicle / companion-computer component (this is what showed up as MAVROS's "MY ID").
- `target_system` / `target_component` in a message = who it's addressed to.

**Heartbeat**
- Every node sends `HEARTBEAT` at 1 Hz to announce it's alive, plus its type/mode/armed state.
- No heartbeat = the other side assumes disconnected. This is exactly what stalled our SITL earlier ("Waiting for heartbeat").

**Versions**
- MAVLink 1 — original, smaller message set.
- MAVLink 2 — more messages, packet signing, extended payloads. What everything modern defaults to.

**Dialects**
- `common.xml` — messages every vehicle understands.
- `ardupilotmega.xml` — ArduPilot-specific extensions on top of common.
- PX4 uses its own extension dialect — part of why PX4 and ArduPilot setups aren't drop-in compatible.

**Messages you'll actually touch**
| Message | Purpose |
|---|---|
| `HEARTBEAT` | Alive signal, vehicle type, armed state |
| `SYS_STATUS` | Battery, sensor health |
| `GLOBAL_POSITION_INT` | Lat/lon/alt |
| `ATTITUDE` | Roll/pitch/yaw |
| `COMMAND_LONG` / `COMMAND_ACK` | Send a command (arm, set mode) + its result |
| `AUTOPILOT_VERSION` | Capability negotiation — the one ArduPilot SITL often doesn't answer |

**Default ports (the thing that actually bit us)**
| Port | Used by |
|---|---|
| `14550` | ArduPilot SITL's default MAVLink/GCS output |
| `14540` | PX4's default offboard/companion port |
| `5760` (TCP) | ArduPilot SITL's raw "serial" master link |

## @MAVROS Bridge — Quick Reference

**What it is:** A ROS/ROS 2 node between MAVLink and ROS. It republishes incoming MAVLink messages as ROS topics, and translates outgoing ROS service/topic calls into MAVLink messages. Built as a set of plugins — each plugin owns one slice of functionality.

**Connecting it**
- `fcu_url` — where the autopilot is: `udp://<bind_host>:<bind_port>@<remote_host>:<remote_port>`. Leave everything after `@` empty to auto-detect the return address instead of guessing a port.
- `gcs_url` — optional second output, lets a real GCS (e.g. QGroundControl) connect at the same time as MAVROS.
- `target_system_id` / `target_component_id` — which vehicle MAVROS treats as "the" FCU (default `1`, `1`).

**Topics you'll check constantly**
| Topic | Tells you |
|---|---|
| `/mavros/state` | Connected? Armed? Current mode — check this first, always |
| `/mavros/battery` | Voltage/percentage — good proof real data is flowing |
| `/mavros/imu/data` | Orientation, angular velocity |
| `/mavros/global_position/global` | GPS fix |
| `/mavros/local_position/pose` | Position in the local ENU frame |

**Services you'll call to control the vehicle**
| Service | Does |
|---|---|
| `/mavros/cmd/arming` (`CommandBool`) | Arm / disarm |
| `/mavros/set_mode` (`SetMode`) | Change flight mode (e.g. `GUIDED`) |
| `/mavros/cmd/takeoff` | Takeoff to altitude |
| `/mavros/cmd/land` | Land |

**Sending setpoints (offboard-style control)**
- `/mavros/setpoint_velocity/cmd_vel`
- `/mavros/setpoint_position/local`
- `/mavros/setpoint_raw/local`

**Gotchas already hit (full detail in your troubleshooting notes)**
- Wrong port → MAVROS never hears a heartbeat at all.
- Hardcoded remote port in `fcu_url` → MAVROS hears the FCU but can't reply (`channel closed`).
- `AUTOPILOT_VERSION` timeout warning is common with ArduPilot and usually harmless — trust `/mavros/state`, not that one warning.

  
## @Troubleshooting notes

| # | Issue | Fix (short) |
|---|-------|-------------|
| 1 | Used PX4's MAVLink port (14540) instead of ArduPilot's | Use `14550` |
| 2 | Fixed remote port in `fcu_url` caused `channel closed` errors | Use `udp://127.0.0.1:14550@` (auto-detect) |
| 3 | `grep` with two words broke the pipe | Use `grep -E 'A\|B'` |
| 4 | `AUTOPILOT_VERSION` warning looked fatal | It's benign — check `/mavros/state` instead |
| 5 | No Gazebo window, SITL frozen on heartbeat | **Open** — GPU rendering suspected |

---

### 1. MAVROS connected to the wrong port (PX4's, not ArduPilot's)
**Mistake:** Used `fcu_url:=udp://:14540@127.0.0.1:14550`.
Port `14540` is PX4 SITL's default MAVLink port, not ArduPilot's —
MAVROS was listening on the wrong port and never received a heartbeat.

**Fix:** ArduPilot SITL sends MAVLink to `14550` by default:
```bash
ros2 run mavros mavros_node --ros-args \
  -p fcu_url:="udp://127.0.0.1:14550@14555" \
  -p target_system_id:=1 \
  -p target_component_id:=1
```

**Lesson:** PX4 and ArduPilot default to different MAVLink ports
(PX4 = 14540, ArduPilot = 14550). Check the SITL terminal's own
startup output for the actual port instead of assuming.

---

### 2. MAVROS could receive but not send (`channel closed` spam)
**Mistake:** Fixed the port above, but kept a hardcoded remote port —
`udp://127.0.0.1:14550@14555`. MAVROS locked onto `14555` as the
address to reply to, but nothing was listening there. Every outbound
packet (heartbeats, version requests) got rejected, logged
repeatedly as:
```
Error: mavconn: udp0: send: channel closed!
    at line 229 in ./src/udp.cpp
```

**Fix:** Drop the fixed remote port and let MAVROS auto-detect the
return address from the first packet it receives:
```bash
ros2 run mavros mavros_node --ros-args \
  -p fcu_url:="udp://127.0.0.1:14550@" \
  -p target_system_id:=1 \
  -p target_component_id:=1
```
(The trailing `@` with nothing after it is intentional, not a typo.)

**Lesson:** Don't manually pin a remote port in `fcu_url` unless you
know for certain the FCU is listening there. Auto-detect (`@` with
nothing after it) is the safer default for SITL.

---

### 3. `grep` "broke" the pipe searching for two things at once
**Mistake:**
```bash
ros2 pkg list | grep turtlesim turtle_teleop_key
```

**Why it looked broken:** `grep PATTERN FILE` treats the *second*
word as a filename to search inside, not a second pattern. grep
tried and failed to open a file called `turtle_teleop_key`, exited
immediately, and closed the pipe — triggering `ros2 pkg list`'s
`BrokenPipeError`. Not a ROS 2 or install problem.

**Fix:**
```bash
ros2 pkg list | grep -E 'turtlesim|teleop'
```
Also: `turtle_teleop_key` is an *executable* inside the `turtlesim`
package, not a package itself — find it with
`ros2 pkg executables turtlesim`.

**Lesson:** Use `grep -E 'A|B'` to search for multiple patterns.
Unrelated to the ArduPilot/MAVROS pipeline itself — just a general
CLI habit worth remembering.

---

### 4. "your FCU don't support AUTOPILOT_VERSION" — looked like an error, wasn't
**Symptom:**
```
[WARN] VER: broadcast request timeout, retries left 4
...
[WARN] VER: your FCU don't support AUTOPILOT_VERSION, switched to default capabilities
```

**Turned out to be:** Not a bug. This is a known, common quirk when
MAVROS talks to ArduPilot SITL specifically — MAVROS asks for exact
capability info, ArduPilot SITL often doesn't answer that particular
request, and MAVROS just falls back to default capabilities. It
fires once at startup, not on a repeating loop.

**How to actually check the link is fine:**
```bash
ros2 topic echo /mavros/state       # look for connected: true
ros2 topic echo /mavros/battery     # real data = real connection
```

**Lesson:** Not every `WARN` in the mavros log means something is
broken — check the concrete `/mavros/state` topic before chasing a
warning that might just be cosmetic.

---

### 5. Gazebo window never opens (OPEN — still debugging)
**Symptom:** All nodes launch with no crash, but no Gazebo GUI window
appears at all. SITL's terminal sits frozen on:
```
Waiting for heartbeat from tcp:127.0.0.1:5760
```

**Current hypothesis:** ArduCopter SITL won't finish booting (and so
never heartbeats) until Gazebo sends it a first physics/sensor
packet. If Gazebo's GUI never actually starts — commonly caused by
hybrid NVIDIA/Intel graphics rendering to the wrong GPU — SITL just
waits forever with no error message.

**Diagnostics in progress:**
```bash
gz sim shapes.sdf                                                              # does Gazebo work at all, standalone?
__NV_PRIME_RENDER_OFFLOAD=1 __GLX_VENDOR_LIBRARY_NAME=nvidia gz sim shapes.sdf # force the NVIDIA GPU
glxinfo | grep "OpenGL renderer"                                               # confirm which GPU is rendering
```

**Status:** Not yet resolved — update this entry once the root cause
is confirmed.

## **Response Video** 
[Screencast from 08-11-2026 02:27:23 AM.webm](https://github.com/user-attachments/assets/04735be0-8f98-4350-a691-b980d266726a)

## **Concepts Mastered**
Quadcopter physics · MAVLink protocol · MAVROS bridge · SITL vs hardware · Flight modes

---

# **M1: MAVROS Communication & Basic Commands**
**Abstraction Layer** — Clean ROS2 API over MAVROS; full vehicle command authority.

**Deliverables**
- Custom interfaces: `DroneState`, `Waypoint`, `ArmDisarm`, `SetMode`, `TakeoffLand`, `ExecuteMission`
- MAVROS wrapper node: state/pose publishers, command services, setpoint publisher
- Verified arm/disarm, mode switching, OFFBOARD entry/exit via ROS2 services

**Concepts Mastered**
ROS2 interfaces (msg/srv/action) · MAVROS service mapping · OFFBOARD requirements · Frame conversion (ENU↔NED) · QoS profiles

---

# **M2: State Estimation & Sensor Fusion**
**Perception** — Fused, high-rate state estimate with covariance.

**Deliverables**
- Complementary filter or EKF fusing IMU + GPS + barometer
- `/quad/state` (DroneState) at 50Hz+ with meaningful covariance
- Sensor quality monitoring and dropout handling

**Concepts Mastered**
Sensor models · Complementary filter / EKF · Noise characterization · Covariance tuning · Time synchronization

---

# **M3: Basic Flight Control (Takeoff/Hover/Land)**
**Control** — Cascaded PID loops achieving stable hover.

**Deliverables**
- Position (outer) → Attitude (inner) → Motor mixer control stack
- Stable hover at target position for 30+ seconds (XY < 0.3m, Z < 0.2m)
- Takeoff → hover → land sequence via service calls
- Emergency stop from any state

**Concepts Mastered**
Cascaded control architecture · PID tuning · Motor mixing (X-config) · Anti-windup · Feedforward (gravity compensation)

---

# **M4: Position Control & Waypoint Navigation**
**Guidance** — Fly arbitrary 3D trajectories with precision.

**Deliverables**
- Waypoint follower with acceptance radius and velocity limits
- Trajectory generator: smooth paths (polynomial splines)
- Predefined missions: square, figure-8, circle
- Dynamic waypoint updates mid-flight

**Concepts Mastered**
Path following (pure pursuit, L1, Stanley) · Trajectory generation · Waypoint acceptance logic · Local↔global coordinate transforms

---

# **M5: Mission System & Autonomy**
**Autonomy** — Complete mission executive with QGroundControl integration.

**Deliverables**
- Mission state machine: IDLE → ARM → TAKEOFF → WAYPOINTS → RTL/LAND
- Action server for `ExecuteMission` with feedback (current WP, ETA)
- Complex missions: survey grid, orbit, region-of-interest
- Pause/resume/abort via ROS2 actions

**Concepts Mastered**
Behavior trees / state machines · MAVLink mission protocol · Action server pattern · Error handling (unreachable WP, timeout)

---

# **M6: Safety Systems & Failsafes**
**Reliability** — Autonomous protection against failures.

**Deliverables**
- Geofence: cylinder/polygon boundary → breach triggers RTL
- Battery monitor: 3-level failsafe (warn → RTL → land now)
- Link loss detection: heartbeat timeout → RTL
- Health monitor: GPS quality, EKF status, sensor health

**Concepts Mastered**
Failsafe hierarchy · Battery modeling · Geofence math · MAVLink heartbeat monitoring

---

# **M7: Integration Testing & Simulation Campaign**
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

# **M8: Hardware Deployment & Real Flight**
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

This project is open source and available under the [MIT License] 

