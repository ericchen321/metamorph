# Instantiate a Franka Arm in Isaac Sim

This doc explains how to instantiate a Franka Arm in Isaac Sim, specify the end-effector's target position, control its joint angles via scripting, read joint angle, velocity and torque values.


## Installing Issac Sim

[Install Issac Sim](https://docs.isaacsim.omniverse.nvidia.com/4.5.0/installation/download.html)

Scroll down and look for version (4.2.0)
- I have not yet tested version 4.0.0 but it should also work fine.

```
mkdir ~/isaacsim
cd ~/Downloads
unzip "isaac-sim-standalone-4.5.0-linux-x86_64.zip" -d ~/isaacsim
cd ~/isaacsim
./omni.isaac.sim.post.install.sh
./isaac-sim.selector.sh
```

Then, we can run an example script which imports the franka arm and sets up positional tracking

```
./python.sh standalone_examples/api/omni.isaac.franka/follow_target_with_rmpflow.py
```

