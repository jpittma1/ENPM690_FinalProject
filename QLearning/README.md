
## Overview

Autonomous robots are the next big thing influencing the tech industry. With tech majors such as google, amazon and apple investing heavily on autonomous tech it is certain that such robots a going to majorly impact our life in the near future. 

When a robot is in an unexplored environment, it does not know the set of best actions to perform for that environment in order to navigate autonomously without colliding. In this software we are taking the example of a turtlebot navigating a maze. While the Turtlebot is in the operating environment, it is nearly impossible to define all possible states, and actions for those states, prior to navigating the full environment. Even if such a case is possible, it may not generalize well for a new environment. Under these circumstances, training the agent with a sequence of rewards for the random actions that it performs, is much easier. This is where Q learning comes into play. The agent is positively rewarded when it performs a desirable actions (not colliding with obstacles), given a state. Similarly, it is negatively rewarded when it performs an undesirable action (like colliding with an obstacle). While using rewards as a learning input, it is easy to define a numerical evaluation function over all states and actions, and base the optimal policy on this evaluation function.

This project will implement a Qlerning algorithm for training a turtlebot to navigate inside a maze (created on gazebo) by avoiding obstacles. The project will show working of the algorithm by using a demo that shows the turtlebot navigating inside the maze without colliding. 


## LICENSE

```
Copyright (c) 2023, Jerry Pittman, Jr., Maitreya Kulkarni
 
Redistribution and use in source and binary forms, with or without  
modification, are permitted provided that the following conditions are 
met:
 
1. Redistributions of source code must retain the above copyright notice, 
this list of conditions and the following disclaimer.
 
2. Redistributions in binary form must reproduce the above copyright 
notice, this list of conditions and the following disclaimer in the   
documentation and/or other materials provided with the distribution.
 
3. Neither the name of the copyright holder nor the names of its 
contributors may be used to endorse or promote products derived from this 
software without specific prior written permission.
 
THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS 
IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, 
THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR 
PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR 
CONTRIBUTORS BE 
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR 
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF 
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS 
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN 
CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) 
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF 
THE POSSIBILITY OF SUCH DAMAGE.

```
## How to Build
Follow the following steps to build the package
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
source devel/setup.bash
cd src
paste this folder in src
cd ..
catkin_make
```

Install Dependencies
```
rosdep install --from-paths src -y --ignore-src
```

## Test
To run test
```
cd ~/catkin_ws/
catkin_make run_tests
rostest qlearning qlearntest.launch
```
## Running Demo
To run the demo
```
cd ~/catkin_ws/
source devel/setup.bash
roslaunch qlearning qlearn.launch
```
Gazebo opens up and terminal provides two options:
1. Train Qtable
2. Test Qtable

Please present 1 and click enter if you want to train.
The programs will ask you to enter the full path of the .csv file you want to store
the final qtable. If the .csv file doesnt exist it will be created or else it will be overwritten.

Now the gazebo simulation will show the turtlebot trying to navigate. The terminal will show
the episode count, cumulative reward and current epsilon value.
Please press ctrl + c to exit from training, the qtable (.csv) file will be saved automatically at the location you specified.

Now rerun the program and select 2 and press enter for testing the trained qtable.
The program will ask you to specify the full path of the trained qtable(.csv) file.
There are two files in this package namely "god_259.csv" and "god_1451.csv" (both available in the qtable folder). The numbers in the file names indicate the number of episodes they have been trained (higher the better). Enter the
full path of the "god_1451.csv" file and press enter. The turtlebot should navigate without colliding
and complete the maze. Press ctrl + c to exit.





## Known Issues/bugs
As evident from the demo program, the maze requires the turtlebot to take only left turns. The sensor on board the turtlebot has a range of about 60 degrees. This software divides the laserscan range into 4 and uses it as the state for the Q-learning algorithm. Since the sensors visibility is towards the front the algorithm does not train well when trained in environments with both left and right turns. 
This is not a deficiency in the algorithm but in the sensor. 
A modification to a sensor with a higher angular range such as Hokuyo would solve the isse.

Sometimes the path entry for qtable during the testing doesnt work (It happens when the computer is underheavy load, for me it happens while running the program while rendering video files). Please fill in the full path in the program (qlearning class->loadQtable function instead of "path" variable)
