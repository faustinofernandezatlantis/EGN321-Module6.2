# Module 6 Assignment 6.2 — Predicted Against Measured

## 1. Overview
This project compares a deterministic temperature prediction model against physical sensor measurements from a 1,800-sample dataset. The goal is to measure the disagreement between predicted and measured values, identify systematic patterns, and propose testable engineering hypotheses to explain the differences.

## 2. Summary Comparison Metrics
- **Total Measured Records:** 1,800
- **Valid Comparable Records (`sensor_status == "OK"`):** 1,747
- **Excluded Records:** 53 (33 MISSING, 14 REJECTED, 6 SUSPICIOUS)
- **Mean Signed Difference (Measured - Predicted):** +1.735 °C
- **Mean Absolute Difference:** 1.735 °C
- **Maximum Absolute Difference:** 2.603 °C

## 3. Plot Interpretation
- **Predicted vs. Measured (`predicted_vs_measured.png`):** The measured temperature profile closely mirrors the periodic trend and dynamics of the predicted model curve. However, the measured line sits systematically above the predicted curve across all time regions.
- **Residual Plot (`residual_difference.png`):** The residual $(\text{Measured} - \text{Predicted})$ remains strictly positive for every valid sample, hovering around a mean offset of +1.735 °C. This non-zero baseline indicates a systematic offset rather than zero-mean random Gaussian noise.

## 4. Plausible Causes & Verification Tests

### Cause 1: Sensor Calibration / Offset Error
- **Supporting Evidence:** The signed difference is positive across all 1,747 valid points (minimum +0.539 °C, mean +1.735 °C), demonstrating a persistent positive baseline shift.
- **Missing Evidence:** Direct calibration data against a certified temperature standard instrument under reference conditions.
- **Verification Test:** Conduct a 2-point ice-bath (0 °C) and boiling-water (100 °C) calibration test using a high-precision reference thermometer to quantify and recalibrate the sensor offset.

### Cause 2: Circuit Board Heat Dissipation / Unmodeled Environment
- **Supporting Evidence:** The sensor is mounted on a PCB where adjacent active microcontrollers generate localized heat, causing the local environment to remain warmer than the ambient temperature modeled by the prediction tool.
- **Missing Evidence:** Separate ambient temperature readings taken away from the main electronics board.
- **Verification Test:** Isolate the temperature sensor on an extension cable inside an isothermal chamber away from the circuit board to verify if the measured temperature drops closer to the predicted value.

## 5. Handling of Invalid Data
A total of 53 rows with status `MISSING`, `REJECTED`, or `SUSPICIOUS` were preserved in the raw dataset but excluded from the residual comparison. No values were interpolated or invented for missing intervals, adhering to the deterministic verification rules.

## 6. AI Log Summary
Local LLM (Ollama / Qwen2.5:0.5b) was used as a review assistant to analyze patterns and draft potential causes. All numerical calculations, data filtering, and plot exports were produced deterministically via Python code.