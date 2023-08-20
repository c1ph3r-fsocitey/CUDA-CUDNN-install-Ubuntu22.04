# Steps for Installation of CUDA v11.36 and cuDNN 8.5 Drivers on Ubuntu 22.04

## Step 1: Check if GPU is CUDA Compatible
```
lspci | grep -i nvidia
```
## Step 2: Remove previous installations
```
sudo apt-get purge nvidia*
sudo apt remove nvidia-*
sudo rm /etc/apt/sources.list.d/cuda*
sudo apt-get autoremove && sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*
```

## Step 3: System update
```
sudo apt-get update
sudo apt-get upgrade
```

## Step 4: (Recommended way)
You can also use the GUI provided by Ubuntu to install  the Nvidia Drivers 

In Ubuntu search for "Additional Drivers", and install the one that's recommended

[Additional_Drivers.webm](https://github.com/c1ph3r-fsocitey/CUDA-CUDNN-install-Ubuntu22.04/assets/109020327/31bca94f-2463-445e-8906-f04d2b61915b)

## Alternative to Step 4:(Install Nvidia Drivers with dependencies) 
```
sudo apt install libnvidia-common-515
sudo apt install libnvidia-gl-515
sudo apt install nvidia-driver-515
```

## Step 5: PreInstall CUDA by fetching keys 
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/3bf863cc.pub
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/ /"
```

## Step 6: Update again
```
sudo apt update
```

## Step 7: Install CUDA 11.7
```
sudo apt install cuda-11-7 
```
## Step 8: Path Setup
```
echo 'export PATH=/usr/local/cuda-11.7/bin:$PATH' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda-11.7/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
source ~/.bashrc
sudo ldconfig
```
## Step 9: Download cuDNN for CUDA v11.7

Use the following link to register and download the cuDNN Driver here: https://developer.nvidia.com/rdp/cudnn-archive
Download the one mentioned for CUDA v11.x

[Nvidia_cuDNN.webm](https://github.com/c1ph3r-fsocitey/CUDA-CUDNN-install-Ubuntu22.04/assets/109020327/16f96bbd-630a-4134-9b13-d0cdd9760bbe)

## Step 10: Install the cuDNN .deb file
After downloading the cuDNN deb file, navigate to the downloads folder
```
cd Downloads
```
And use the following command to install it
```
sudo apt install ./<name_of_file.deb>
```

## Step 11: Copy file paths
use the following commands to copy the files to CUDA toolkit directory
```
sudo cp -P cuda/include/cudnn.h /usr/local/cuda-11.7/include
sudo cp -P cuda/lib/libcudnn* /usr/local/cuda-11.7/lib64/
sudo chmod a+r /usr/local/cuda-11.7/lib64/libcudnn*
```
## Step 12: Verify the installation
```
nvidia-smi
nvcc -V
```
## Expected Output for nvidia-smi

![image](https://github.com/c1ph3r-fsocitey/CUDA-CUDNN-install-Ubuntu22.04/assets/109020327/3dde08ee-99a2-4354-8286-b7a873e72500)

## Expected output for nvcc -V

![image](https://github.com/c1ph3r-fsocitey/CUDA-CUDNN-install-Ubuntu22.04/assets/109020327/0a19a403-4203-42a5-a015-faa786eea838)






