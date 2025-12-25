# Model Weights Archive

This folder contains the trained weights for the Jassid Damage Detection model.

## Files
- `best.pt`: PyTorch weights. Use this for further fine-tuning or development in Google Colab.
- `best.onnx`: Exported format for high-speed inference on edge devices (Raspberry Pi/Jetson).

## How to Load
To use these weights in your scripts:

```python
from ultralytics import YOLO

# Load the PyTorch model
model = YOLO('models/best.pt')

# Run inference
results = model.predict('image.jpg', conf=0.15)