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
https://github.com/unitreerobotics/unitree_sdk2_python

## Error during setup
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
