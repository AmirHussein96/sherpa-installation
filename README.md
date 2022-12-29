# K2/sherpa installation

### Prerequisite:
- Please install conda or any other environment management system 
- Create new environtment with python 3.8 `conda create -n k2 python=3.8`
- Install cmake using pip, in my case I installed `pip install cmake==3.18`

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
**Note:** when installing cuda toolkit it might happens that the system will pull and install the latest drivers (in my case cuda 12) although you intended to install cuda 11.3. Double check that the folder  /usr/local/cuda-11.3 was created if not then try installing it again but without drivers.
when I run nvidia-smi:
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 525.60.13    Driver Version: 525.60.13    CUDA Version: 12.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:0A:00.0  On |                  N/A |
| 47%   30C    P8    28W / 350W |   2333MiB / 12288MiB |      9%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1206      G   /usr/lib/xorg/Xorg                153MiB |
|    0   N/A  N/A      1511      G   /usr/bin/gnome-shell               31MiB |
|    0   N/A  N/A      2822      G   /usr/lib/firefox/firefox          134MiB |
|    0   N/A  N/A     11610      G   ...veSuggestionsOnlyOnDemand       79MiB |
|    0   N/A  N/A     47844      C   python3                          1928MiB |
+-----------------------------------------------------------------------------+
```

### Install pytorch 
- First I show details of my installed pytorch env 
```
Collecting environment information...
PyTorch version: 1.12.0
Is debug build: False
CUDA used to build PyTorch: 11.3
ROCM used to build PyTorch: N/A

OS: Ubuntu 20.04.5 LTS (x86_64)
GCC version: (Ubuntu 9.4.0-1ubuntu1~20.04.1) 9.4.0
Clang version: Could not collect
CMake version: version 3.18.0
Libc version: glibc-2.31

Python version: 3.8.15 (default, Nov 24 2022, 15:19:38)  [GCC 11.2.0] (64-bit runtime)
Python platform: Linux-5.15.0-56-generic-x86_64-with-glibc2.17
Is CUDA available: True
CUDA runtime version: 11.3.109
GPU models and configuration: GPU 0: NVIDIA GeForce RTX 3080 Ti
Nvidia driver version: 525.60.13
cuDNN version: Probably one of the following:
/usr/lib/x86_64-linux-gnu/libcudnn.so.8.7.0
/usr/lib/x86_64-linux-gnu/libcudnn_adv_infer.so.8.7.0
/usr/lib/x86_64-linux-gnu/libcudnn_adv_train.so.8.7.0
/usr/lib/x86_64-linux-gnu/libcudnn_cnn_infer.so.8.7.0
/usr/lib/x86_64-linux-gnu/libcudnn_cnn_train.so.8.7.0
/usr/lib/x86_64-linux-gnu/libcudnn_ops_infer.so.8.7.0
/usr/lib/x86_64-linux-gnu/libcudnn_ops_train.so.8.7.0
/usr/local/cuda-11.3/targets/x86_64-linux/lib/libcudnn.so.8.7.0
/usr/local/cuda-11.3/targets/x86_64-linux/lib/libcudnn_adv_infer.so.8.7.0
/usr/local/cuda-11.3/targets/x86_64-linux/lib/libcudnn_adv_train.so.8.7.0
/usr/local/cuda-11.3/targets/x86_64-linux/lib/libcudnn_cnn_infer.so.8.7.0
/usr/local/cuda-11.3/targets/x86_64-linux/lib/libcudnn_cnn_train.so.8.7.0
/usr/local/cuda-11.3/targets/x86_64-linux/lib/libcudnn_ops_infer.so.8.7.0
/usr/local/cuda-11.3/targets/x86_64-linux/lib/libcudnn_ops_train.so.8.7.0
HIP runtime version: N/A
MIOpen runtime version: N/A
Is XNNPACK available: True

Versions of relevant libraries:
[pip3] numpy==1.22.4
[pip3] torch==1.12.0+cu113
[pip3] torchaudio==0.12.0+cu113
[pip3] torchvision==0.13.0+cu113
[conda] blas                      1.0                         mkl  
[conda] cudatoolkit               11.3.1               h2bc3f7f_2  
[conda] mkl                       2022.1.0           hc2b9512_224  
[conda] numpy                     1.22.4                   pypi_0    pypi
[conda] pytorch                   1.12.0          py3.8_cuda11.3_cudnn8.3.2_0    pytorch
[conda] pytorch-mutex             1.0                        cuda    pytorch
[conda] torch                     1.12.0+cu113             pypi_0    pypi
[conda] torchaudio                0.12.0+cu113             pypi_0    pypi
[conda] torchvision               0.13.0+cu113             pypi_0    pypi
```
I installed the following version:
`conda install pytorch==1.12.0 torchvision==0.13.0 torchaudio==0.12.0 cudatoolkit=11.3 -c pytorch`


### install lhotse
- You can check the details here https://lhotse.readthedocs.io/en/latest/getting-started.html#installation
- This worked for me `pip install git+https://github.com/lhotse-speech/lhotse`


### Install k2
- Refer to the documentation for more details [https://kaldifeat.readthedocs.io/en/latest/installation.html#install-kaldifeat-from-source](https://k2-fsa.github.io/k2/installation/index.html)
- You can also check the issues that I raised on github https://github.com/k2-fsa/k2/issues/1124
- Steps I followed:
1. clone the repo
```
git clone https://github.com/k2-fsa/k2.git
cd k2
mkdir build_debug
cd build_debug
```

2. Define pointers to cuda
```
CUDNN_LIBRARY_PATH=/usr/local/cuda-11.3/lib64
CUDNN_INCLUDE_PATH=/usr/local/cuda-11.3/include
```
3. run cmake
```
cmake\
 -DCMAKE_BUILD_TYPE=Debug \
 -DCMAKE_CUDA_COMPILER=$(which nvcc) \
 -DPYTHON_EXECUTABLE=$(which python) \
 -DCUDNN_LIBRARY_PATH=$CUDNN_LIBRARY_PATH/libcudnn.so \
 -DCUDNN_INCLUDE_PATH=$CUDNN_INCLUDE_PATH \
 ..
```
4. run `make -j8`
5. add k2 to python path

```
K2_ROOT=/speech/toolkits/k2
export PYTHONPATH=$K2_ROOT/k2/python:$PYTHONPATH
export PYTHONPATH=$K2_ROOT/build_debug/lib:$PYTHONPATH
```
6. to check k2 installed succesfully run `python -m k2.version` 

### Install kaldifeat
- Refer to the documentation for more details https://kaldifeat.readthedocs.io/en/latest/installation.html#install-kaldifeat-from-source
- You can also check the issues that I raised on github https://github.com/csukuangfj/kaldifeat/issues/59
- Steps I followed:
1. clone the repo
```
git clone https://github.com/csukuangfj/kaldifeat
cd kaldifeat
mkdir build
cd build
```
2. run cmake
```
cmake\
 -DCMAKE_BUILD_TYPE=Debug \
 -DCMAKE_CUDA_COMPILER=$(which nvcc) \
 -DPYTHON_EXECUTABLE=$(which python) \
 -DCUDNN_LIBRARY_PATH=$CUDNN_LIBRARY_PATH/libcudnn.so \
 -DCUDNN_INCLUDE_PATH=$CUDNN_INCLUDE_PATH \
 ..
 ```
 
3. run `make -j8`
4. add kaldifeat to python path
```
kfeat=/speech/toolkits/kaldifeat
export PYTHONPATH=$kfeat/kaldifeat/python:$PYTHONPATH
export PYTHONPATH=$kfeat/build/lib:$PYTHONPATH
```
5. to check kaldifeat installed succesfully run `python3 -c "import kaldifeat; print(kaldifeat.__version__)"` 

**Note:**
- Make sure you got kaldilm 1.11 not 1.14 since this also caused issues https://github.com/k2-fsa/icefall/issues/794

### Install sherpa
- Refer to the documentation for more details [https://kaldifeat.readthedocs.io/en/latest/installation.html#install-kaldifeat-from-source](https://k2-fsa.github.io/sherpa/python/installation/from-source.html#install-sherpa)
- You can also check the issues that I raised on github [https://github.com/csukuangfj/kaldifeat/issues/59](https://github.com/k2-fsa/sherpa/issues/258) and https://github.com/k2-fsa/sherpa/issues/257
- Steps I followed:
1. clone the repo
```
git clone https://github.com/k2-fsa/sherpa
cd sherpa
```
2. export k2 and kaldifeat path
```
export K2_INSTALL_PREFIX=/speech/toolkits/k2/build_debug
export KALDIFEAT_INSTALL_PREFIX=/speech/toolkits/kaldifeat/build
```
- **Method 1**
3. pip install -r ./requirements.txt
4. **Note** Make sure that you either installed kaldifeat with pip or from source but not both. If you have both remove the one installed with pip `pip uninstall kaldifeat`
5. python3 setup.py install --verbose
6. To check the installation run `python3 -c "import sherpa; print(sherpa.__version__)"`
7. Follow the steps here to run the server with a pretrained model https://k2-fsa.github.io/sherpa/python/streaming_asr/conformer/conformer_rnnt_for_English/index.html


- **Method 2** If you want to use sherpa in command line
3. Specify cudnn path and run cmake

```
CUDNN_LIBRARY_PATH=/usr/local/cuda-11.3/lib64
CUDNN_INCLUDE_PATH=/usr/local/cuda-11.3/include
```

4. run cmake and then make
```
cmake  -DCMAKE_BUILD_TYPE=Release  -DCMAKE_INSTALL_PREFIX=$HOME/software/sherpa  
-DCMAKE_CUDA_COMPILER=$(which nvcc)  -DPYTHON_EXECUTABLE=$(which python)  -DCUDNN_LIBRARY_PATH=$CUDNN_LIBRARY_PATH/libcudnn.so  -DCUDNN_INCLUDE_PATH=$CUDNN_INCLUDE_PATH  ..

make -j6 install/strip
```
5. export the path to sherpa
`export PATH=$HOME/software/sherpa/bin:$PATH`
```
4. To check the installation run 
`sherpa-version`

The output will be somethig similar to below
```

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
