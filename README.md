# Speed, Acceleration, Jerk

Derive kinematic features from keypoint time series.

## Data layout
Inputs:
- `data/raw/sample1_body.csv`  # body keypoints
- `data/raw/sample1.mp4`       # optional video (not required by CLI)

Expected columns: per-joint axes named like `WRIST_x, WRIST_y, WRIST_z`.  
A time column is optional. If absent, set `--fs`.

## Environment
conda env create -f environment.yml
conda activate kinematics

## CLI
# magnitude-only features for all joints
python scripts/kinematics.py \
  --in data/raw/sample1_body.csv \
  --out results/sample1_features.csv \
  --fs 30

# specify a time column (seconds) instead of --fs
python scripts/kinematics.py \
  --in data/raw/sample1_body.csv \
  --out results/sample1_features.csv \
  --time-col t

# include per-axis derivatives and limit to x,y axes
python scripts/kinematics.py \
  --in data/raw/sample1_body.csv \
  --out results/sample1_features.csv \
  --fs 30 --axes x y --per-axis

## Notebook
jupyter lab
# open notebooks/01-Gesture_Kinematic_Analysis.ipynb