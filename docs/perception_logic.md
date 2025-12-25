# Perception Logic: YOLOv8 + SAHI

### The Ground Sample Distance (GSD) Problem
At a flight altitude ($H$) of 30ft (~9.14m), the resolution of a single pixel on the ground (GSD) is calculated as:

$$GSD_w = \frac{H \times S_w}{F \times I_w}$$

Where:
- $H$: Flight Altitude
- $S_w$: Sensor Width (mm)
- $F$: Focal Length (mm)
- $I_w$: Image Width (pixels)

### Why we use SAHI (Tiling)
Standard YOLOv8 downsamples input images to 640x640. If a 4000x3000 drone image is downsampled, tiny jassid damage clusters (often < 20 pixels) vanish. 

**Our Solution:** We use 416px slices with a 40% overlap. This ensures that the AI "sees" the leaf texture at its native resolution, maintaining our **1.00 Background Precision**.