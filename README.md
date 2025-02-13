# Ubuntu-NVIDIA-Setup

## Introduction
A comprehensive guide for installing and configuring NVIDIA drivers, CUDA, and CUDNN on Ubuntu systems, including additional setup for other essential applications.

## NVIDIA Driver:
```bash
sudo apt update
sudo apt upgrade
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install ubuntu-drivers-common
ubuntu-drivers devices
sudo apt install nvidia-driver-520
reboot
```
To verify the installation, use: ```nvidia-smi```

if your GPU are 40 series, to do A part.
if your GPU are others, you can choose A or B part.
Because the lowest CUDA version for 40 series is 11.8.

## A part
A1. **NVIDIA CUDA:**

```bash
sudo apt update
sudo apt upgrade
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2004-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update

sudo apt-get -y install cuda
or
sudo apt-get -y install cuda-toolkit-11-8
```

```bash
gedit ~/.bashrc
export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64\${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

To verify the installation, use: ```nvcc -V```

A2. **NVIDIA CUDNN:**
GO to this link Download
https://developer.nvidia.com/downloads/compute/cudnn/secure/8.8.1/local_installers/11.8/cudnn-local-repo-ubuntu2004-8.8.1.3_1.0-1_amd64.deb/

```bash
sudo dpkg -i cudnn-local-repo-ubuntu2004-8.8.1.3_1.0-1_amd64.deb
sudo cp /var/cudnn-local-repo-ubuntu2004-8.8.1.3/cudnn-local-CCF73F15-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt -y upgrade
sudo apt-get update
sudo apt-get install libcudnn8=8.8.1.3-1+cuda11.8 
sudo apt-get install libcudnn8-dev=8.8.1.3-1+cuda11.8 
sudo apt-get install libcudnn8-samples=8.8.1.3-1+cuda11.8 
sudo apt-get -y install libfreeimage3 libfreeimage-dev
reboot
```

## B part

B1. **NVIDIA CUDA:**

```bash
sudo apt update
sudo apt upgrade
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.7.1/local_installers/cuda-repo-ubuntu2004-11-7-local_11.7.1-515.65.01-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2004-11-7-local_11.7.1-515.65.01-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2004-11-7-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda
```

```bash
gedit ~/.bashrc
export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64\${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

To verify the installation, use: ```nvcc -V```

B2. **NVIDIA CUDNN:**
Go to this link to Download
https://developer.nvidia.com/compute/cudnn/secure/8.4.1/local_installers/11.6/cudnn-local-repo-ubuntu2004-8.4.1.50_1.0-1_amd64.deb

```bash
sudo dpkg -i cudnn-local-repo-ubuntu2004-8.4.1.50_1.0-1_amd64.deb
sudo cp /var/cudnn-local-repo-ubuntu2004-8.4.1.50/cudnn-local-E3EC4A60-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt -y upgrade
sudo apt-get update
sudo apt-get install libcudnn8=8.4.1.50-1+cuda11.6
sudo apt-get install libcudnn8-dev=8.4.1.50-1+cuda11.6
sudo apt-get install libcudnn8-samples=8.4.1.50-1+cuda11.6
sudo apt-get -y install libfreeimage3 libfreeimage-dev
reboot
```

3. **To verify the CUDNN installation, use:**
```bash
cp -r /usr/src/cudnn_samples_v8 ~/Documents/
cd Documents/cudnn_samples_v8/mnistCUDNN/
make clean && make
./mnistCUDNN

You will see "Test Pass"
```

4. **To verify the installation, use:**
```bash
cat /usr/include/x86_64-linux-gnu/cudnn_v*.h | grep CUDNN_MAJOR -A 2
```

5. **Other Application**
```bash
sudo apt -y install htop
sudo apt -y install ibus-chewing
sudo apt -y install terminator

```

6. **Two Systeam Time**
```bash
sudo timedatectl set-local-rtc 1
sudo apt-get install ntpdate
sudo ntpdate time.windows.com
sudo hwclock --localtime --systohc
```

## References

- **Two Systeam Time**: [Two Systeam Time](https://www.796t.com/content/1547213953.html)
- **Install NVIDIA Driver**: [Eric Chang](https://gitpress.io/@chchang/install-nvidia-driver-cuda-pgstrom-in-ubuntu-1804?fbclid=IwAR1gJ3958FijQNoPvTkqJ5IF2BmKr_FnvjDgVtXpe37EXWb)
- **NVIDIA CUDA**: [CUDA Download](https://developer.nvidia.com/cuda-11-7-1-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&t)
- **NVIDIA CUDNN**: [CUDNN Download](https://developer.nvidia.com/rdp/cudnn-archive)
- **NVIDIA CUDNN Guide**: [CUDNN Installation Guide](https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html)
- **NVIDIA CUDA Guide**: [CUDA Installation Guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/)
- **Debug**: ['libcudnn8' was not found](https://forums.developer.nvidia.com/t/e-version-8-3-1-22-1-cuda10-2-for-libcudnn8-was-not-found/200801)
