# Flight Testing Logs

### Test Environment
- **Location:** [Insert Field Location]
- **Target Pest:** Jassid (Amrasca biguttula)
- **Drone Altitude:** 30ft Constant (Nadir View)

### Performance Summary
| Metric | Value | Interpretation |
| :--- | :--- | :--- |
| mAP@.5 | 0.41 | High for small-object agricultural detection. |
| Precision | 1.00 | Zero false positives on healthy canopy. |
| Recall | 0.44 | Conservative detection; improved via SAHI. |

### Observations
1. **Lighting:** High-noon sun creates shadows that increase background noise. 
2. **Wind:** Drone pitch during gusts affects the IK solver accuracy; recommend using a 3-axis gimbal for stabilization.