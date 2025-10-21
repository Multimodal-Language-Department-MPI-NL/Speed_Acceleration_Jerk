# Gesture Kinematic Features: Speed, Acceleration, Jerk

## Attribution

The custom functions for smoothing and calculating speed vectors and derivatives are sourced from the following EnvisionBox module: **Selecting, smoothing, and deriving measures from motion tracking, and merging with acoustics and annotations in Python**.

If you found this code helpful for your research, please cite the original source code material from the EnvisionBox website:

**Pouw, W. (2023).** *Selecting, smoothing, and deriving measures from motion tracking, and merging with acoustics and annotations.* [21.10.2025]. Retrieved from: https://envisionbox.org/embedded_MergingMultimodal_inPython.html

---

This module shows how to calculate movement speed. It also calculates acceleration (changes in speed over time) and jerk (e.g., sudden movements) which are derivatives of speed. 

## 🔬 Research Context

Part of the gesture analysis pipeline. This module derives motion dynamics after optional normalization and smoothing, enabling robust comparison across speakers and sessions.

## 🎯 What This Project Does

1. **Load keypoints**: Read body landmark time series (X, Y, Z per landmark)
2. **Normalize coordinates (optional)**: Shoulder-centered, shoulder-width scaled
3. **Smooth trajectories**: Zero-phase Butterworth low-pass filter
4. **Derive kinematics**: Speed, vertical velocity, acceleration, jerk
5. **Visualize**: Interactive plots for quick inspection

## 📊 Smoothing Process

1. **Begin with Cleaned Data**: Prefer smoothed/normalized input from upstream modules
2. **Inspect**: Plot key axes and landmarks to assess noise and trends
3. **Apply Smoothing**: Zero-phase low-pass filtering of positions and/or derivatives
4. **Compute Derivatives**: Finite differences with optional smoothing of results
5. **Evaluate & Save**: Visualize and export features for downstream tasks

## 🔧 Smoothing Techniques

- **Normalization**: Shoulder-midpoint centering; scaled by shoulder distance (notebook)
- **Smoothing**: Butterworth low-pass, zero-phase via `filtfilt`
- **Speed**: Euclidean displacement per time unit
- **Vertical velocity**: First derivative of Y
- **Acceleration**: First derivative of speed
- **Jerk**: First derivative of acceleration
- **Feature scaling (optional)**: Z-score to comparable ranges

## 📁 Project Structure

```
Speed_Acceleration_Jerk/
├── README.md
├── environment.yml
├── notebooks/
│   └── Gesture_Kinematic_Analysis.ipynb
├── scripts/
│   └── kinematics.py                 # CLI placeholder (WIP)
├── src/
│   └── kinematics/
│       └── __init__.py
├── sample1.mp4                       # Example video (optional)
└── results/
```

## 🚀 Quick Start

### Prerequisites

```bash
conda env create -f environment.yml
conda activate kinematics
```

### Run the Interactive Notebook

```bash
jupyter lab
# Open notebooks/Gesture_Kinematic_Analysis.ipynb
```


## 📈 Data Format

### Input
- **CSV files**: Columns for each landmark coordinate, e.g., `X_RIGHT_INDEX, Y_RIGHT_INDEX, Z_RIGHT_INDEX`, plus `time` if available

### Output
- **In-notebook variables/plots**: Derived features and visualizations
- **Optional CSV export**: Feature tables for modeling/analysis

## 🎛️ Configuration

- **Sampling rate (`fs`)**: Frames per second for derivatives
- **Butterworth**: `order`, `lowpass_cutoff`
- **Feature selection**: Landmark(s) and axes to derive from

## 🔗 Related Projects

- `https://github.com/Multimodal-Language-Department-MPI-NL/MediaPipe_keypoints_extraction`
- `https://github.com/Multimodal-Language-Department-MPI-NL/Smoothing`
- `https://github.com/Multimodal-Language-Department-MPI-NL/Normalization`

## 📖 References

- Pouw, W. (2023). Selecting, smoothing, and deriving measures from motion tracking. `https://envisionbox.org/embedded_MergingMultimodal_inPython.html`