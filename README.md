## ESP32_ros2
ROS2 driver for ESP32 Micro-controllers.

## 1. Installation
### 1.1 Install the ROS2 driver and its dependencies:

    cd <your_ws>
    git clone https://github.com/grassjelly/atom_matrix_ros2 src/atrom_matrix_ros2
    rosdep install --from-paths src -i -r -y
    colcon build
    
    

## 2. Installing the firmware

### 2.1 Install PlatformIO (only have to do once)

    python3 -c "$(curl -fsSL https://raw.githubusercontent.com/platformio/platformio/master/scripts/get-platformio.py)"
    echo "PATH=\"\$PATH:\$HOME/.platformio/penv/bin\"" >> $HOME/.bashrc
    source $HOME/.bashrc

### 2.2 Install the firmware to the Atom Matrix

    cd atom_matrix_ros2/firmware
    pio run --target upload
    
### 2.3  Install https://github.com/surfertas/ros2_ipcamera

    sudo apt install rospack-tools ros-humble-cv-bridgelibcamera-info-manager0d libcamera-info-manager-dev

    git clone https://github.com/surfertas/ros2_ipcamera.git
    colcon build --symlink-install
    . install/setup.bash

## 3. Running the driver

### 3.1 
Add sourcing to your shell startup script
    echo "source /opt/ros/dashing/setup.bash" >> ~/.bashrc

Run the launch file to run the [microROS agent](https://github.com/micro-ROS/micro-ROS-Agent) and [IMU Madgwick Filter](https://index.ros.org/p/imu_filter_madgwick/)

    ros2 launch atom_matrix_ros2 imu.launch

Optional arguments

**rviz**  - If you want to run rviz and visualize the filter's estimated pose. For example:

    ros2 Launch atom_matrix_ros2 imu.launch rviz:=true
