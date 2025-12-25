# Navigation & Control Stack

This module handles the autonomous movement of the UAV and the precise targeting of hardware sensors based on AI-detected pest clusters.

## 🏗️ System Architecture
The navigation stack operates on a **Perception-Action Loop**:
1. **Target Acquisition:** `perception/` module identifies jassid damage coordinates in image space $(u, v)$.
2. **Coordinate Transformation:** `kinematics/` converts pixel data to physical world coordinates $(X, Y, Z)$.
3. **Motion Planning:** `path_planning/` generates optimal waypoints for scouting or hovering.
4. **Execution:** `controllers/` sends MAVLink commands to the flight controller via DroneKit.

## 📂 Module Breakdown

### 1. Kinematics (`/kinematics`)
- **`ik_solver.py`**: Solves the Inverse Kinematics for a 2-DOF gimbal/arm. It calculates the necessary joint angles ($\theta_1, \theta_2$) to center the sensor on a detected hotspot.
- **Math Model:** Uses the geometric approach (Law of Cosines) to avoid high-computational overhead during flight.



### 2. Path Planning (`/path_planning`)
- **`waypoint_gen.py`**: Implements a "Dynamic Scouting" logic. 
    - *Default:* Lawn-mower search pattern.
    - *Interrupt:* If jassid density > threshold, the drone deviates to perform a localized "Orbit" or "Spiral" scan for high-res data capture.

### 3. Controllers (`/controllers`)
- **`drone_interface.py`**: The bridge to the Pixhawk/ArduPilot hardware.
- **Safety Protocol:** Includes automated failsafes for GPS loss, low battery, and geofence breaches.

## 🛰️ Integration with NASA Requirements
To meet precision agriculture standards, this stack maintains a **Ground Sample Distance (GSD)** of 2.5mm/px by dynamically adjusting the drone's Z-axis (altitude) based on real-time terrain feedback.



## 🛠️ Testing in SITL
To test without risking hardware:
1. Launch ArduPilot SITL.
2. Run the wrapper:
   ```bash
   python navigation/controllers/drone_interface.py --connect udp:127.0.0.1:14550