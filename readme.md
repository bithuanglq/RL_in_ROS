### 本地配置
Ubuntu20.04   
Gazebo-11   
ROS-noetic   

```
mkdir ~/catkin_ws
cd catkin_ws
mkdir src
cd src
git clone git@github.com:bithuanglq/RL_in_ROS.git
cd ..
catkin_make
```


### 提示
代码参考： https://blog.csdn.net/qq_33361420/article/details/118222009

1. gym from 0.26.2 to 0.19.0

2. 修改 openai_examples_projects/my_turtlebot3_openai_example/config/my_turtlebot3_openai_qlearn_params_v2.yaml 第三行为自己的 catkin 包路径

3. roslaunch my_turtlebot3_openai_example start_training_v2.launch

4. 可能 noetic 版本影响的只是 turtlebot(模型包) 模型编译，因为 openai_ros(地图包) 和 openai_examples_projects(RL算法) 包不受影响；逻辑关系是这样的，openai_ros在GazeboEnvironment下定义了多个RobotEnvironment，openai_examples_projects根据RobotEnvironment定义多个TaskEnvironment，每个TaskEnvironment下包含强化学习(RL)算法和训练代码

5. 在 openai_examples_projects/my_turtlebot3_openai_example/scripts/ 下修改 RL 算法和训练代码

6. 自定义任务环境就是重写一个与src/openai_ros/task_envs目录下相似的环境类， 在定义好环境类后，需要在src/openai_ros/task_envs/task_envs_list.py文件中，将自定义的环境注册到gym中。简单理解就是给你定义的环境命名，可以通过openai_ros.openai_ros_common.StartOpenAI_ROS_Environment函数得到自定义的环境

7. openai_ros 中 turtlebot2 需要下载[turtlebot](https://bitbucket.org/theconstructcore/turtlebot.git)包，但默认的TaskEnvironment配置是 kinetic-gazebo9
```
cd ~/catkin_ws/src
git clone https://bitbucket.org/theconstructcore/turtlebot.git
cd turtlebot
git checkout kinetic-gazebo9
```

