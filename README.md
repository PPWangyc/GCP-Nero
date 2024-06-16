
# Google Cloud Platform — Stanford Nero

## Quick Start Guide

1.  Connect to Stanford VPN
2.  Create an Instance
3.  SSH Login
4.  NVIDIA Driver & CUDA Toolkit Installation
5.  Install Anaconda

## 1. Connect to Stanford VPN

Refer to the detailed documentation on [Nero GCP](https://nero-docs.stanford.edu/). You must have a Stanford account and be connected to su.vpn.stanford.edu (Full Tunnel). For VPN download and access instructions, please visit [Stanford VPN Information](https://uit.stanford.edu/service/vpn).

## 2. Create an Instance

First, determine the required machine type and compute resources. Then, log in to the Google Cloud Platform to create your virtual machine. For detailed instructions, refer to the [GCP Instance Creation Guide](https://cloud.google.com/compute/docs/instances/create-start-instance).

## 3. SSH Login

To access the VM instance created in the previous step, it is recommended to use an SSH Key for quick access. First, generate a private and public key pair. You can do this either through the [Google Console](https://cloud.google.com/compute/docs/connect/add-ssh-keys) or on your local machine as shown below:

`ssh-keygen -t rsa -f ~/.ssh/KEY_FILENAME -C USERNAME -b 2048` 

Then, add the public key to your VM.

## 4. NVIDIA Driver & CUDA Toolkit

Skip this section if GPU compute resources are not required. For detailed installation instructions, refer to [GCP NVIDIA Drivers](https://cloud.google.com/compute/docs/gpus/install-drivers-gpu#install-script). A simple script installation via Python is recommended. Ensure Python3 is installed beforehand. Download and run the installation script as follows:

Download the script:

`curl -L https://github.com/GoogleCloudPlatform/compute-gpu-installation/releases/download/cuda-installer-v1.0.0/cuda_installer.pyz --output cuda_installer.pyz` 

Run the installation script (note that the script may restart your VM):

`sudo python3 cuda_installer.pyz install_driver` 

Check the driver installation status:

`nvidia-smi` 

To install the toolkit and verify the installation, use:

`sudo python3 cuda_installer.pyz install_cuda
sudo python3 cuda_installer.pyz verify_cuda` 

## 5. Install Anaconda

Anaconda is a versatile tool for managing your development environments. For quick installation instructions, see this [Anaconda Installation Guide](https://developers.google.com/earth-engine/guides/python_install-conda).

To make conda be initialized in default terminal. Add code below in your bash script:

    # >>> conda initialize >>>
    # !! Contents within this block are managed by 'conda init' !!
    __conda_setup="$('/home/ppwang/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
    if [ $? -eq 0 ]; then
        eval "$__conda_setup"
    else
        if [ -f "/home/ppwang/miniconda3/etc/profile.d/conda.sh" ]; then
            . "/home/ppwang/miniconda3/etc/profile.d/conda.sh"
        else
            export PATH="/home/ppwang/miniconda3/bin:$PATH"
        fi
    fi
    unset __conda_setup
    # <<< conda initialize <<< 

