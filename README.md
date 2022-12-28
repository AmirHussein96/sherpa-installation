# K2/icefall/sherpa installation

install Cuda11.3 
`https://gist.github.com/Mahedi-61/2a2f1579d4271717d421065168ce6a73`

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
