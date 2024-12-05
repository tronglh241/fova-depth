# FOVA-Depth Setup Guide

## 1. Create a Conda Environment
Create a new Conda environment named `fova-depth` with Python 3.10 and activate it:
```bash
conda create -n fova-depth python=3.10 -y && conda activate fova-depth
```

## 2. Install PyTorch
Install PyTorch and TorchVision with CUDA 11.8 support:
```bash
pip install torch torchvision --index-url https://download.pytorch.org/whl/cu118
```

## 3. Install System Dependencies
Update the system packages and install the required dependencies:
```bash
apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    pkg-config \
    libglvnd0 \
    libgl1 \
    libglx0 \
    libegl1 \
    libgles2 \
    libglvnd-dev \
    libgl1-mesa-dev \
    libegl1-mesa-dev \
    libgles2-mesa-dev \
    cmake \
    curl
```

## 4. Install GCC (version 9 or higher)
Install GCC and G++ version 9 from the Conda Forge channel:
```bash
conda install -c conda-forge gcc=9 gxx=9
```

## 5. Set Environment Variables
Configure environment variables for Python and OpenGL:
```bash
export PYTHONDONTWRITEBYTECODE=1
export PYTHONUNBUFFERED=1
export LD_LIBRARY_PATH=/usr/lib64:$LD_LIBRARY_PATH
export PYOPENGL_PLATFORM=egl
```

## 6. Copy NVIDIA Configuration File
If the `10_nvidia.json` file does not exist, copy it to the appropriate location:
```bash
cp docker/10_nvidia.json /usr/share/glvnd/egl_vendor.d/10_nvidia.json
```

## 7. Install Python Dependencies
Install Python packages and external dependencies:
```bash
pip install ninja imageio imageio-ffmpeg
```

### Install NVDiffrast
Prepare and install the `nvdiffrast` package:
```bash
pip install externals/nvdiffrast/
```

### Additional Python Packages
Install the remaining dependencies:
```bash
pip install nvTorchCam/
pip install -r requirements.txt
```

