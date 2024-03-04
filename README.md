
## Ubuntu configuration

### 1. gcc configuration.
```bash
sudo apt-get update
sudo apt-get upgrade -y
sudo apt install gcc-10 g++-10 -y
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-10 100 --slave /usr/bin/g++ g++ /usr/bin/g++-10 
```
### 2. downloading of runtime cuda package, installing of nvidia driver and verification of installation.

```bash
wget https://developer.download.nvidia.com/compute/cuda/11.3.0/local_installers/cuda_11.3.0_465.19.01_linux.run
sudo sh cuda_11.3.0_465.19.01_linux.run --silent --driver
nvidia-smi
```
### 3. installation of cuda compiler and adding it to PATH permanently.
> [!CAUTION]
> You need to ignore text "This installation did not install the CUDA Driver. A driver of version at least 465.00 is required for CUDA 11.3 functionality to work."

```
sudo sh cuda_11.3.0_465.19.01_linux.run
nano ~/.bashrc
```
### 4. append next lines to the file.
```
export PATH=/usr/local/cuda-11.3/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-11.3/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```
### 5. and apply it!
```
source ~/.bashrc
nvcc -V
```
### 6. downloading of conda
```
wget https://repo.anaconda.com/archive/Anaconda3-2021.11-Linux-x86_64.sh
bash Anaconda3-2021.11-Linux-x86_64.sh
```
> [!IMPORTANT]
> Installer will ask you about terms and .... directory  of installtion.
> You need to type your user home directory.
> it can be default, but recheck it please

---
> [!IMPORTANT]
> now you need to REBOOT your Ubuntu.


### 7. creating and activationg of conda env
```
conda create -n Py39_Torch1.10_cu11.3 python=3.9 -y
conda activate Py39_Torch1.10_cu11.3
```
### 8. installation of requirements 
```
pip3 install torch==1.10.1+cu113 torchvision==0.11.2+cu113 torchaudio==0.10.1+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html

```
### 9. clonning and installation yolov5_obb repo
```
git clone https://github.com/hukaixuan19970627/yolov5_obb
cd yolov5_obb/utils/nms_rotated
python setup.py develop
cd ../..
python detect.py
```