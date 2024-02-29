# DiffOcclusion: Differentiable Optimization Based Control Barrier Functions for Occlusion-Free Visual Servoing

This repository contains the code for the paper "DiffOcclusion: Differentiable Optimization Based Control Barrier Functions for Occlusion-Free Visual Servoing" by Shiqing Wei, Bolun Dai, Rooholla Khorrambakht, Prashanth Krishnamurthy, and Farshad Khorrami, published in IEEE Robotics and Automation Letters (RA-L). 

Take a look at our [paper](https://ieeexplore.ieee.org/document/10430369) and [video](https://youtu.be/su0RPjcBwOc)!

## Pre-requisites/Installation
Create a new conda environment (with python3.8) and install the packages by running the following command:
```bash
conda env create -f environment.yml
```

If this does not work, you can manually install the following packages in a python 3.8 environment: 
```bash
pip install cvxpy cvxpylayers torch torchvision torchaudio opencv-python proxsuite pybullet apriltag julia gymnasium
```

We also need [pinocchio](https://github.com/stack-of-tasks/pinocchio), the installation of which depends on your platform.

Note: julia is only required by our [previous work](https://differentiableoptimizationcbf.readthedocs.io/en/latest/install.html).

## Usage
First, cd into the directory of the repository:
```bash
cd DiffOcclusion
```

To reproduce simulation 1 in our paper, run the following command:
```bash 
python visual_servoing_dob_collision/box_under_dob_normalized.py
```

To reproduce simulation 2 in our paper, run the following command:
```bash
python visual_servoing_dob_collision/square_around_dob_normalized.py
```

## Robot Collision Avoidance 
If you want to use the physical collision avoidance functionalities of our work, uncomment the following lines in `box_under_dob_normalized.py` (or `square_around_dob_normalized.py`):
```
if platform == "darwin":
    print("==> Initializing Julia")
    time1 = time.time()
    from julia.api import Julia
    jl = Julia(compiled_modules=False)
    time2 = time.time()
    print("==> Initializing Julia took {} seconds".format(time2-time1))
```
and 
```
try:
    from differentiable_collision_utils.dc_cbf import DifferentiableCollisionCBF
except:
    from differentiable_collision_utils.dc_cbf import DifferentiableCollisionCBF
```

Then, set `"active": 1` in `collision_cbf_config` of `test_settings_001.json` (or `test_settings_002.json`) located in `visual_servoing_dob_collision/test_settings`:
```
"collision_cbf_config":{
    "active": 1,
    ...
}
```

## Citation
If you use this code for your research, please cite our paper:
```
@ARTICLE{10430369,
  author={Wei, Shiqing and Dai, Bolun and Khorrambakht, Rooholla and Krishnamurthy, Prashanth and Khorrami, Farshad},
  journal={IEEE Robotics and Automation Letters}, 
  title={DiffOcclusion: Differentiable Optimization Based Control Barrier Functions for Occlusion-Free Visual Servoing}, 
  year={2024},
  volume={9},
  number={4},
  pages={3235-3242},
  keywords={Visualization;Optimization;Visual servoing;Shape;Robot sensing systems;Systematics;Robot kinematics;Visual servoing;visual tracking;robot safety;sensor-based control},
  doi={10.1109/LRA.2024.3364468}}
```
