# Installation


## Requirements

### Core library

The core library is written in PyTorch. Several components have underlying implementation in CUDA for improved performance. A subset of these components have CPU implementations in C++/PyTorch. It is advised to use PyTorch3D with GPU support in order to use all the features.

- Linux or macOS or Windows
- Python 3.8, 3.9 or 3.10
- PyTorch 1.12.0, 1.12.1, 1.13.0, 2.0.0, 2.0.1 or 2.1.0.
- torchvision that matches the PyTorch installation. You can install them together as explained at pytorch.org to make sure of this.
- gcc & g++ ≥ 4.9
- [fvcore](https://github.com/facebookresearch/fvcore)
- [ioPath](https://github.com/facebookresearch/iopath)
- If CUDA is to be used, use a version which is supported by the corresponding pytorch version and at least version 9.2.
- If CUDA older than 11.7 is to be used and you are building from source, the CUB library must be available. We recommend version 1.10.0.

The runtime dependencies can be installed by running:
```
conda create -n pytorch3d python=3.9
conda activate pytorch3d
conda install pytorch=1.13.0 torchvision pytorch-cuda=11.6 -c pytorch -c nvidia
conda install -c fvcore -c iopath -c conda-forge fvcore iopath
```

For the CUB build time dependency, which you only need if you have CUDA older than 11.7, if you are using conda, you can continue with
```
conda install -c bottler nvidiacub
```
Otherwise download the CUB library from https://github.com/NVIDIA/cub/releases and unpack it to a folder of your choice.
Define the environment variable CUB_HOME before building and point it to the directory that contains `CMakeLists.txt` for CUB.
For example on Linux/Mac,
```
curl -LO https://github.com/NVIDIA/cub/archive/1.10.0.tar.gz
tar xzf 1.10.0.tar.gz
export CUB_HOME=$PWD/cub-1.10.0
```

## Building / installing from source.
CUDA support will be included if CUDA is available in pytorch or if the environment variable
`FORCE_CUDA` is set to `1`.

### 1. Install from GitHub
```
pip install "git+https://github.com/TheNeeloy/pytorch3d.git"
```

For CUDA builds with versions earlier than CUDA 11, set `CUB_HOME` before building as described above.

**Install from Github on macOS:**
Some environment variables should be provided, like this.
```
MACOSX_DEPLOYMENT_TARGET=10.14 CC=clang CXX=clang++ pip install "git+https://github.com/TheNeeloy/pytorch3d.git"
```

### 2. Install from a local clone
```
git clone https://github.com/TheNeeloy/pytorch3d.git
cd pytorch3d && pip install -e .
```
To rebuild after installing from a local clone run, `rm -rf build/ **/*.so` then `pip install -e .`. You often need to rebuild pytorch3d after reinstalling PyTorch. For CUDA builds with versions earlier than CUDA 11, set `CUB_HOME` before building as described above.

**Install from local clone on macOS:**
```
MACOSX_DEPLOYMENT_TARGET=10.14 CC=clang CXX=clang++ pip install -e .
```

**Install from local clone on Windows:**

Depending on the version of PyTorch, changes to some PyTorch headers may be needed before compilation. These are often discussed in issues in this repository.

After any necessary patching, you can go to "x64 Native Tools Command Prompt for VS 2019" to compile and install
```
cd pytorch3d
python3 setup.py install
```

After installing, you can run **unit tests**
```
python3 -m unittest discover -v -s tests -t .
```
