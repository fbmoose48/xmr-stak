# Compile **xmr-stak-rx** for Linux

## Install Dependencies

### AMD Driver (only needed to use AMD GPUs)

- the AMD APP SDK is not longer needed (all is included in the driver package)
- download & unzip the AMD driver: https://www.amd.com/en/support
- run `./amdgpu-pro-install --opencl=legacy,pal` from the unzipped folder
- set the environment variable to opencl `export AMDAPPSDKROOT=/opt/amdgpu-pro/`

For linux also the OpenSource driver ROCm 1.9.X+ is a well working alternative, see https://rocm.github.io/ROCmInstall.html
ROCm is not supporting old GPUs please check if your GPU is supported https://rocm.github.io/hardware.html.

### Cuda 8.0+ (only needed to use NVIDIA GPUs)

- download and install [https://developer.nvidia.com/cuda-downloads](https://developer.nvidia.com/cuda-downloads)
- for minimal install choose `Custom installation options` during the install and select
    - CUDA/Develpment
    - CUDA/Runtime
    - Driver components

### GNU Compiler
```
    # Ubuntu / Debian
    sudo apt install libmicrohttpd-dev libssl-dev cmake build-essential libhwloc-dev ocl-icd-opencl-dev
    git clone https://github.com/fbmoose48/xmr-stak.git -b xmr-stak-rx
    mkdir xmr-stak/build
    cd xmr-stak/build
    cmake ..
    make install

    # Arch
    sudo pacman -S --needed base-devel hwloc openssl cmake libmicrohttpd
    git clone https://github.com/fbmoose48/xmr-stak.git -b xmr-stak-rx
    mkdir xmr-stak/build
    cd xmr-stak/build
    cmake ..
    make install
```

- g++ version 5.1 or higher is required for full C++11 support.

- Some newer gcc versions are not supported by CUDA (e.g. Ubuntu 17.10). It will require installing gcc 5 but you can avoid changing defaults.

In that case you can force CUDA to use an older compiler in the following way:
```
cmake -DCUDA_HOST_COMPILER=/usr/bin/gcc-5 ..
```

- You need 1 Gb RAM to compile (a bit less might be enough, 512 Mb isn't). 

### To do a generic and static build for a system without gcc 5.1+
```
    cmake -DCMAKE_LINK_STATIC=ON -DXMR-STAK_COMPILE=generic .
    make install
```
Note - cmake caches variables, so if you want to do a dynamic build later you need to specify '-DCMAKE_LINK_STATIC=OFF'

# Compile **Xmr-Stak-RX** for FreeBSD

## Install Dependencies

*Note: This guide is tested for FreeBSD 11.0-RELEASE*

From the root shell, run the following commands:

    pkg install git libmicrohttpd hwloc cmake

Type 'y' and hit enter to proceed with installing the packages.

    git clone https://github.com/fbmoose48/xmr-stak.git -b xmr-stak-rx
    mkdir xmr-stak/build
    cd xmr-stak/build
    cmake ..
    make install

Now you have the binary located at "bin/" and the needed shared libraries.

