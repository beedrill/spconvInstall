# SPCONV Library installation
At time 2021/4/10, SPCONV is **EXTREMELY** hard to install (current version 1.2). The library is not rapidly supported and there are very few installation isntruction. So I put a record here. The version of library is:
- Ubuntu 18.04
- Cuda 10.2
- Cudnn 7.6.5
- cmake 3.18.4
- gcc 7.5.0
- Python 3.7
- Pytorch 1.6.0
Need to use exactly these combination, any version higher or lower might cause problem (I eventually get passed when update Cuda from 10.1 to 10.2)..

## steps
1. use a clean new Ubuntu 18.04 OS
2. `sudo apt update && sudo apt upgrade`
3. `sudo ubuntu-drivers autoinstall`
4. Install Cuda 10.2.89 (they say 10.1.234 also work but there is only 10.1.105 online and that version will NOT work), installation can be found [here](https://developer.nvidia.com/cuda-10.2-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=runfilelocal):
```
wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
sudo sh cuda_10.2.89_440.33.01_linux.run
```
After installation, remember to follow its printout message to update **PATH** and **LD_LIBRARY_PATH**
5. Install Cudnn, the version MUST be [7.6.5](https://developer.nvidia.com/compute/machine-learning/cudnn/secure/7.6.5.32/Production/10.2_20191118/cudnn-10.2-linux-x64-v7.6.5.32.tgz), the guide can be found [here](https://docs.nvidia.com/deeplearning/cudnn/archives/cudnn_765/cudnn-install/index.html#installlinux-tar), must be installed from tar.
```bash
$ sudo cp cuda/include/cudnn.h /usr/local/cuda/include
$ sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
$ sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```
7. install Anaconda, and create new environment with python 3.7:
```
conda create -n spconv python=3.7
conda activate spconv
```
8. install Pytorch, version 1.6.0
```
conda install pytorch==1.6.0 torchvision==0.7.0 cudatoolkit=10.2 -c pytorch
```
9.Once all these are done, you can follow the guide on sponv repo and finish the installation:
```
git clone xxx.git --recursive
sudo apt-get install libboost-all-dev
pip install cmake
python setup.py bdist_wheel
cd dist
pip install xxx.whl

```