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

## Set up unitree_sdk2_python
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
