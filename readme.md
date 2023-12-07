### 本地配置
Ubuntu20.04   
Gazebo-11   
ROS-noetic   


### 提示
参考： https://blog.csdn.net/qq_33361420/article/details/118222009

1. gym from 0.26.2 to 0.19.0

2. 修改 openai_examples_projects/my_turtlebot3_openai_example/config/my_turtlebot3_openai_qlearn_params_v2.yaml 第三行为自己的 catkin 包路径

3. roslaunch my_turtlebot3_openai_example start_training_v2.launch

4. 可能 noetic 版本影响的只是 turtlebot(模型包) 模型编译，因为 openai_ros(地图包) 和 openai_examples_projects(RL算法) 包不受影响；逻辑关系是这样的，openai_ros在GazeboEnvironment下定义了多个RobotEnvironment，openai_examples_projects根据RobotEnvironment定义多个TaskEnvironment，每个TaskEnvironment下包含强化学习(RL)算法和训练代码

5. 在 openai_examples_projects/my_turtlebot3_openai_example/scripts/ 下修改 RL 算法和训练代码

6. 自定义任务环境就是重写一个与src/openai_ros/task_envs目录下相似的环境类， 在定义好环境类后，需要在src/openai_ros/task_envs/task_envs_list.py文件中，将自定义的环境注册到gym中。简单理解就是给你定义的环境命名，可以通过openai_ros.openai_ros_common.StartOpenAI_ROS_Environment函数得到自定义的环境

### 问题
目前根据[教程](http://wiki.ros.org/openai_ros/TurtleBot2%20with%20openai_ros)自创openai_example_projects/my_turtlebot2_training运行报错：
```
[WARN] [1701940145.567084]: Env: MyTurtleBot2Wall-v0 will be imported
[WARN] [1701940145.635348]: Register of Task Env went OK, lets make the env...MyTurtleBot2Wall-v0
[WARN] [1701940145.677305]: Package NOT FOUND, lets Download it...
[ERROR] [1701940209.843776]: Package turtlebot_gazebo NOT FOUND by ROS.
[ERROR] [1701940209.847578]: IMPORTANT!: You need to execute the following commands and rerun to dowloads to take effect.
[ERROR] [1701940209.850076]: 
In a new Shell:::>
cd /home/hlq/catkin_ws
catkin_make
source devel/setup.bash
rospack profile

[ERROR] [1701940209.852281]: 
In your deeplearning program execute shell catkin_ws:::>
cd /home/user/catkin_ws
source devel/setup.bash
rospack profile

```

有待解决！！！
