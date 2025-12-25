# Autonomous Agricultural Pest Detection & Robotics Pipeline

[![Drone Project CI](https://github.com/akkified/DWU-NASA/actions/workflows/ci.yml/badge.svg)](https://github.com/akkified/DWU-NASA/actions)

## Project Overview
This repository contains a full-stack autonomous drone solution for detecting and reacting to Jassid (pest) damage in agricultural fields. The project integrates **Computer Vision (YOLOv8 + SAHI)** with **Inverse Kinematics** to allow a drone to identify stress clusters from 30ft and adjust its hardware (gimbal/sensors) for precise data collection.

## AI Perception System
Detecting tiny pests from high altitudes creates a "Small Object Problem." Standard inference often fails due to resolution downsampling.

### Sliced Aided Hyper Inference (SAHI)
To maintain a high **Recall (0.44)** and **Precision (1.00)**, we utilize a tiling strategy:
- **Model:** YOLOv8 (Trained on custom Jassid damage dataset)
- **Strategy:** 416px Slices with 40% Overlap
- **mAP:** 0.41 (Optimized for Ground Sample Distance at 30ft)



## Navigation & Kinematics
The system translates pixel coordinates from the AI model into physical motor movements.

### Inverse Kinematics (IK) Solver
Located in `navigation/kinematics/`, the IK engine calculates the required joint angles to point sensors at detected "hotspots."
- **Input:** Target $(x, y)$ coordinates from detection boxes.
- **Output:** Servo/Gimbal angles $(\theta_1, \theta_2)$ using Jacobian-based solvers.



## Repository Structure
- `perception/`: YOLOv8 + SAHI detection scripts.
- `navigation/`: Inverse Kinematics and Path Planning algorithms.
- `models/`: Trained `.pt` and `.onnx` checkpoints.
- `.github/`: CI/CD workflows for code safety and testing.

## Setup & Installation
1. Clone the repo:
   ```bash
   git clone [https://github.com/akkifiedE/DWU-NASA.git](https://github.com/akkifiedE/DWU-NASA.git)

2. Install dependencies: 
   ```bash
   pip install -r requirements.txt

3. Run inference:
   ```bash
   python perception/src/detector.py --source test_image.jpg


Note: This research is being developed for NASA-related agricultural monitoring applications.