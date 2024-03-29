# 터틀봇을 활용한 실내자율주행로봇

> ## PC와 RPI Set-up
+ remote PC</br>
     + ROS 설치(melodic)</br>
     <pre>
        <code>
            sudo apt update
            sudo apt upgrade
            wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_melodic.sh
            chmod 755 ./install_ros_melodic.sh 
            bash ./install_ros_melodic.sh
        </code>
     </pre>
     + Depandent ROS 패키지 설치</br>
    <pre>
        <code>
            sudo apt-get install ros-melodic-joy ros-melodic-teleop-twist-joy ros-melodic-teleop-twist-keyboard ros-melodic-laser-proc ros-melodic-rgbd-launch ros-melodic-depthimage-to-laserscan ros-melodic-rosserial-arduino ros-melodic-rosserial-python ros-melodic-rosserial-server ros-melodic-rosserial-client ros-melodic-rosserial-msgs ros-melodic-amcl ros-melodic-map-server ros-melodic-move-base ros-melodic-urdf ros-melodic-xacro ros-melodic-compressed-image-transport ros-melodic-rqt-image-view ros-melodic-gmapping ros-melodic-navigation ros-melodic-interactive-markers
        </code>
    </pre>
    + Turtlebot3 패키지 설치(melodic)</br>
    <pre>
        <code>
          cd ~/catkin_ws/src/
          git clone -b melodic-devel https://github.com/ROBOTIS-GIT/DynamixelSDK.git
          git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
          git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
          cd ~/catkin_ws && catkin_make
          echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
        </code>
    </pre>
    + RPI 마스터 설정</br>
    <pre>
        <code>
          export ROS_MASTER_URI=http://{IP_ADDRESS_OF_REMOTE_PC}:11311
          export ROS_HOSTNAME={IP_ADDRESS_OF_RASPBERRY_PI_3}
        </code>
    </pre>
    + LDS-02 driver</br>
    <pre>
        <code>
          sudo apt update
          sudo apt install libudev-dev
          cd ~/catkin_ws/src
          git clone -b develop https://github.com/ROBOTIS-GIT/ld08_driver.git
          cd ~/catkin_ws/src/turtlebot3 && git pull
          rm -r turtlebot3_description/ turtlebot3_teleop/ turtlebot3_navigation/ turtlebot3_slam/ turtlebot3_example/
          cd ~/catkin_ws && catkin_make
        </code>
    </pre>
    
    
> ## SLAM    
    +remote PC</br>
    <pre>
        <code>
          roscore
          export TURTLEBOT3_MODEL=burger
          roslaunch turtlebot3_slam turtlebot3_slam.launch
          roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
          rosrun map_server map_saver -f ~/map
        </code>
    </pre>
    
> ## Navigation    
    +remote PC</br>
    <pre>
        <code>
          roscore
          export TURTLEBOT3_MODEL=burger
          roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
        </code>
    </pre>   

    






    
      
