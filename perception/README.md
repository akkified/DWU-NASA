# Perception Module: Small Object Detection

## Overview
This module specializes in detecting **jassid damage** from aerial imagery. Because the targets are small (often <1% of the total image area), standard inference is replaced with a **Sliced Aided Hyper Inference (SAHI)** pipeline.

## Pipeline
1. **Input:** High-resolution drone image (e.g., 4000x3000).
2. **Tiling:** Image is divided into 416x416 overlapping patches.
3. **Inference:** `models/best.pt` (YOLOv8) runs on each patch.
4. **Reconstruction:** Detections are merged back into the original coordinate space.

## Performance
- **Model:** YOLOv8s
- **Precision:** 1.00 (Crucial for avoiding false chemical applications)
- **mAP:** 0.41 (Validated on 30ft altitude datasets)