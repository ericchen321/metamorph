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

## Querying Joint Angles, Joint Velocity, and Joint Torque

Querying joint angles via python is very simple.

```
# Get object franka arm object from scene
my_franka = my_world.scene.get_object(franka_name)

# Get controller which defines articulation of robot (can be any controller)
my_controller = RMPFlowController(name="target_follower_controller", robot_articulation=my_franka)

# While the simulation is playing
while simulation_app.is_running():
    # Have controller articulate robot
    actions = my_controller.forward(
        target_end_effector_position=observations[target_name]["position"],
        target_end_effector_orientation=observations[target_name]["orientation"],
    )

    # actions now holds all the updated joint data of robot
    joint_data = actions.get_dict()
    print("Joint Angle (Radians):", joint_data['joint_positions'])
    print("Joint Velocity:", joint_data['joint_velocities'])
    print("Joint Torque:", joint_data['joint_efforts'])
```


## Specifying end-effector's target position

There are two ways to set the end-target position of the franka arm. This is either through inverse kinematics, or through [RMPFlow](https://www.youtube.com/watch?v=Fl4WvsXQDzo)

**RMP Flow**

You can launch an example script that sets up a scene with the franka arm, set to follow a target cube using RMP Flow:

```
./python.sh standalone_examples/api/omni.isaac.franka/follow_target_with_rmpflow.py
```

**IK**

You can launch an example script that sets up a scene with the franka arm, set to follow a target cube using IK:

```
./python.sh standalone_examples/api/omni.isaac.franka/follow_target_with_ik.py
```


