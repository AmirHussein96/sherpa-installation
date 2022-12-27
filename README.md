# K2/icefall/sherpa installation



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
