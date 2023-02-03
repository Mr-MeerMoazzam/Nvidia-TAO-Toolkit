
# Install TAO Toolkit on PC

TAO Toolkit is used to build extremely accurate, customizable, and production-ready AI models to power your speech and computer vision AI applications.

In this repo, you will see how to install the TAO Toolkit.






## Requirements

### Hardware Requirements
To get adequate training performance with TAO Toolkit and the supporting models given, the following system configuration is recommended.

 - 32 GB system RAM
 - 32 GB of GPU RAM
 - 8 core CPU
 - 1 NVIDIA GPU
 - 100 GB of SSD space

On discrete GPUs such as the H100, A100, A40, A30, A2, A16, A100x, A30x, V100, T4, Titan-RTX, and Quadro-RTX, TAO Toolkit is supported.

Note: Prior to the Pascal generation, TAO Toolkit was not supported by GPUs.

### Software Requirements

| Software | Version |  Comment |
| --- | --- | --- |
| `Ubuntu LTS` | 20.04 | |
| `Python` | >=3.6.9<3.7 | Not needed if you are using TAO API |
| `Docker-ce` | >19.03.5 | Not needed if you are using TAO API |
| `Docker-API` | 1.40| Not needed if you are using TAO API |
| `nvidia-container-toolkit` | >1.3.0-1 | Not needed if you are using TAO API |
| `nvidia-container-runtime` | 3.4.0-1 | Not needed if you are using TAO API |
| `nvidia-docker2` | 2.5.0-1 | Not needed if you are using TAO API |
| `nvidia-driver` | >520 | Not needed if you are using TAO API |
| `python-pip` |  >21.06	 | Not needed if you are using TAO API |

## Package Content

Download the TAO package, which includes startup scripts, Jupyter notebooks, and configuration files. TAO is also supported on Google Colab; if you wish to try on Colab, you can skip this step and go straight to the [Running on Google Colab](https://docs.nvidia.com/tao/tao-toolkit/text/running_in_cloud/running_tao_toolkit_on_google_colab.html#id1). Otherwise, follow below instructions.



```bash
wget --content-disposition https://api.ngc.nvidia.com/v2/resources/nvidia/tao/tao-getting-started/versions/4.0.0/zip -O getting_started_v4.0.0.zip
unzip -u getting_started_v4.0.0.zip  -d ./getting_started_v4.0.0 && rm -rf getting_started_v4.0.0.zip && cd ./getting_started_v4.0.0

```


## Running TAO Toolkit

Both a docker container and a set of python wheels are options for the TAO toolkit. Depending on your setup and preferences, there are 4 methods to launch TAO Toolkit:

- the launcher CLI

- the containers directly

- the tao toolkit apis

- python wheels

Running TAO toolkit through launcher CLI is an easy and beginner friendly method so that we will use this method to run TAO Toolkit.

### Launcher CLI

The TAO Toolkit launcher is a simple command-line interface written in Python. The launcher serves as a user interface for TAO Toolkit containers developed on top of PyTorch and TensorFlow. The CLI hides from the user which network is implemented in which container. Depending on the model you intend to employ, the relevant container is launched automatically.

Follow the steps listed below to instal the necessary prerequisite applications before using the launcher.

#### Installing the prerequisites
The TAO Toolkit launcher is a Python3 package that can run on Python versions >= 3.6.9.

##### 1. Install `docker-ce`  
For the installation of docker-ce you can follow the [Official Instructions](https://docs.docker.com/engine/install/). After setting up docker-ce, make sure the docker can be run without sudo by following the [post-installation instructions](https://docs.docker.com/engine/install/linux-postinstall/).

##### 2. Install `nvidia-container-toolkit`
The following is a list of requirements for installing the NVIDIA Container Toolkit:
######  1. GNU/Linux x86_64 with kernel version > 3.10
######  2. Docker >= 19.03 (recommended, but some distributions may include older versions of Docker. The minimum supported version is 1.12)
######  3. NVIDIA GPU with Architecture >= Kepler (or compute capability 3.0)
######  4. NVIDIA Linux drivers >= 418.81.07 (Note that older driver releases or branches are unsupported.)
######  5. Setup the package repository and the GPG key

```bash
distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
      && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
      && curl -s -L https://nvidia.github.io/libnvidia-container/experimental/$distribution/libnvidia-container.list | \
         sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
         sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
```
###### 6. Install the nvidia-docker2 package (and dependencies) after updating the package listing

```bash
sudo apt-get update
```
```bash
sudo apt-get install -y nvidia-docker2
```
After setting the default runtime, restart the Docker daemon to complete the installation:

```bash
sudo systemctl restart docker
```

A functioning setup can now be checked by running the following CUDA container:

```bash
sudo docker run --rm --gpus all nvidia/cuda:11.6.2-base-ubuntu20.04 nvidia-smi
```
This should produce the following console output:

```bash
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 450.51.06    Driver Version: 450.51.06    CUDA Version: 11.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla T4            On   | 00000000:00:1E.0 Off |                    0 |
| N/A   34C    P8     9W /  70W |      0MiB / 15109MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+

```
## Acknowledgements

 - [Official Documentation](https://catalog.ngc.nvidia.com/orgs/nvidia/teams/tao/resources/tao-getting-started)
