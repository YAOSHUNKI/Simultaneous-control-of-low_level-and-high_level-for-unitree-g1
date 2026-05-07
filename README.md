# Simultaneous-control-of-low_level-and-high_level-for-unitree-g1
This document describes how to perform both high-level and low-level control simultaneously using the unitree g1.\
This is a testing phase designed to control walking at the high-level and arm movement at the low-level.

##  reference
・https://github.com/unitreerobotics/unitree_ros2 \
・https://github.com/KobeKosenRobotics/rosenv_for_unitree \
・https://github.com/unitreerobotics/unitree_sdk2_python

# Set up 
For information on the environment, please refer to the following repository \
https://github.com/KobeKosenRobotics/rosenv_for_unitree#reference \
https://github.com/unitreerobotics/unitree_sdk2_python \
https://github.com/YAOSHUNKI/unitree-g1-high_level-ros2


# Test
## Terminal 1
```bash
ros2 run unitree_ros2_example g1_high_level_ros2
```
## Terminal 2
```bash
python3 /home/colcon_ws/src/unitree_sdk2_python/example/g1/high_level/g1_arm7_sdk_dds_example.py eth0
```

## Error during test
### the APT repository is missing a signature key
If the APT repository is missing a signature key
```bash
NO_PUBKEY FB0B24895113F120
```
If you encounter this error, please run the following script
```bash
sudo apt install -y gnupg
sudo mkdir -p /etc/apt/keyrings
sudo gpg --keyserver keyserver.ubuntu.com --recv-keys FB0B24895113F120
sudo gpg --export FB0B24895113F120 | sudo tee /etc/apt/keyrings/fix.gpg > /dev/null
```
### ModuleNotFoundError: No module named 'cyclonedds'
If you encounter an error like this when running an .src file, please run the following command:
```bash
export CYCLONEDDS_HOME=/usr/local
export CMAKE_PREFIX_PATH=/usr/local
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
```
Please enter the following command to verify that CycloneDDS has been installed
```bash
ls /usr/local/lib | grep dds
```
If the result looks like this, the installation was successful.
```bash
libddsc.so
libddscxx.so
```
If it works, please update the version.
```bash
python3 -m pip uninstall -y cyclonedds
python3 -m pip install "cyclonedds==0.10.2"
```
### ImportError: cannot import name 'b2'
Please edit init.py
```bash
vi /home/colcon_ws/install/unitree_sdk2py/lib/python3.10/site-packages/unitree_sdk2py/__init__.py
```
Before revision:
```bash
from . import idl, utils, core, rpc, go2, b2
```
After revision:
```bash
from . import idl, utils, core, rpc, go2
```
### cannot open shared object file: No such file or directory
Find the lib directory
```bash
find /home/colcon_ws/src/unitree_sdk2_python -name "crc_aarch64.so"
```
Create a directory in the `install` directory
```bash
mkdir -p /home/colcon_ws/install/unitree_sdk2py/lib/python3.10/site-packages/unitree_sdk2py/utils/lib
```
.so copy
```bash
cp /home/colcon_ws/src/unitree_sdk2_python/unitree_sdk2py/utils/lib/crc_aarch64.so \
/home/colcon_ws/install/unitree_sdk2py/lib/python3.10/site-packages/unitree_sdk2py/utils/lib/
```
