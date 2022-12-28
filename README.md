# K2/icefall/sherpa installation

### Prerequisite:
- Please install conda or any other environment management system 
- Create new environtment with python 3.8 `conda create -n k2 python=3.8`

### Install GCC
- Check this link for which GCC should be installed before installing Cuda
https://stackoverflow.com/questions/6622454/cuda-incompatible-with-my-gcc-version

- This tutorial also was helpful to install gcc and set the correct version
https://linuxize.com/post/how-to-install-gcc-on-ubuntu-20-04/

- check that you installed the required gcc version by running `gcc --version`


### install Cuda toolkit and Cudnn
- I tried cuda toolkit 10.2, gcc 6.3 for older Ubuntu 18.04, and Cuda 11.3, gcc 9.4 for Ubuntu 20 but others might work as well.
- To install cuda toolkit and Cudnn follow the instruction here https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html#download
- I followed the steps below to install cuda 11.3 toolkit
`https://gist.github.com/Mahedi-61/2a2f1579d4271717d421065168ce6a73`
- Make sure to point to the correct cuda directory by running the commands below:
```
export CUDA_HOME=/usr/local/cuda-11.3  # currently links to /opt/NVIDIA/cuda-10,>
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.3/lib64:/usr/local/cuda-11.3/extras/CUPTI/lib64
export PATH="$CUDA_HOME/bin:$PATH"
```
- To make sure cuda you are pointing to the correct cuda run `nvcc -V`, it should print
```
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Mon_May__3_19:15:13_PDT_2021
Cuda compilation tools, release 11.3, V11.3.109
Build cuda_11.3.r11.3/compiler.29920130_0
```

###



Note
sherpa installation steps:
1- export k2 and kaldifeat path
```
export K2_INSTALL_PREFIX=/speech/toolkits/k2/build_debug
export KALDIFEAT_INSTALL_PREFIX=/speech/toolkits/kaldifeat/build
```

2- Specify cudnn path and run cmake

```
CUDNN_LIBRARY_PATH=/usr/local/cuda-11.3/lib64
CUDNN_INCLUDE_PATH=/usr/local/cuda-11.3/include

cmake  -DCMAKE_BUILD_TYPE=Release  -DCMAKE_INSTALL_PREFIX=$HOME/software/sherpa  
-DCMAKE_CUDA_COMPILER=$(which nvcc)  -DPYTHON_EXECUTABLE=$(which python)  -DCUDNN_LIBRARY_PATH=$CUDNN_LIBRARY_PATH/libcudnn.so  -DCUDNN_INCLUDE_PATH=$CUDNN_INCLUDE_PATH  ..

make -j6 install/strip

export PATH=$HOME/software/sherpa/bin:$PATH
```
3- To check the installation run 
`sherpa-version`

The output will be somethig similar to below

```
sherpa version: 1.1
build type: Release
OS used to build sherpa: Ubuntu 20.04.5 LTS
sherpa git sha1: 7bc4ea22d4ef611795522e20ccebf44f0df1f961
sherpa git date: Wed Dec 21 04:12:34 2022
sherpa git branch: master
PyTorch version used to build sherpa: 1.12.0
CUDA version: 11.3
cuDNN version: 8.7.0
k2 version used to build sherpa: 1.23.2
k2 git sha1: a34171ed85605b0926eebbd0463d059431f4f74a
k2 git date: Tue Dec 13 11:06:38 2022
k2 with cuda: ON
kaldifeat version used to build sherpa: 1.22
cmake version: 3.18.0
compiler ID: GNU
compiler: /usr/bin/c++
compiler version: 9.4.0
cmake CXX flags:    -Wall  -g  -D_GLIBCXX_USE_CXX11_ABI=0   -D_GLIBCXX_USE_CXX11_ABI=0 -Wno-unused-variable  -Wno-strict-overflow   -D_GLIBCXX_USE_CXX11_ABI=0
```
