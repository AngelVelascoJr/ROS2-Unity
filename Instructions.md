# ROS2-Unity connection

this pkg contains part of the Unity-Ros2 demo pkg to comunicate ros2 with unity

# prerequisites

In order to use this pkg, you need:
- an unity proyect with the ROS_TCP_CONECTOR pkg, the instructions to download it are in the [Unity-Robotics-hub](https://github.com/Unity-Technologies/Unity-Robotics-Hub)
- Ros2

## Usage

This instructions are from the [ros_unity_integration setup tutorial](https://github.com/Unity-Technologies/Unity-Robotics-Hub/blob/main/tutorials/ros_unity_integration/setup.md#ros2-environment) for ros2

1. run the next commands in the terminal 

    ``` bash

    source install/setup.bash
    colcon build
    source install/setup.bash

    ```

    Note: yes, you need to run the source command twice. The first sets up the environment for the build to use, the second time adds the newly built packages to the environent.

2. In your Colcon workspace, run the following command, replacing `<your IP address>` with your ROS machine's IP or hostname.

	```bash
	ros2 run ros_tcp_endpoint default_server_endpoint --ros-args -p ROS_IP:=<your IP address>
    ```

   - If you're running ROS in a Docker container, 0.0.0.0 is a valid incoming address, so you can write `ros2 run ros_tcp_endpoint default_server_endpoint --ros-args -p ROS_IP:=0.0.0.0`
   - On Linux you can find out your IP address with the command `hostname -I`
   - On MacOS you can find out your IP address with `ipconfig getifaddr en0`

   Once the server_endpoint has started, it will print something similar to `[INFO] [1603488341.950794]: Starting server on 192.168.50.149:10000`.

3. (Alternative) If you need the server to listen on a port that's different from the default 10000, here's the command line to also set the ROS_TCP_PORT parameter:

	```bash
	ros2 run ros_tcp_endpoint default_server_endpoint --ros-args -p ROS_IP:=127.0.0.1 -p ROS_TCP_PORT:=10000
	```

after that, you can continue with the unity scene setup for a publisher node found [here](https://github.com/Unity-Technologies/Unity-Robotics-Hub/blob/main/tutorials/ros_unity_integration/publisher.md)

to test the publisher, you only need to listen to the topic:

``` bash
source install/setup.bash
ros2 topic echo pos_rot
```
